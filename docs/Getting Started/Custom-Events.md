# Creating custom events / RPCs

Horizon server allows you to easily add your own custom events via a system of file organization. This system consists of the ``linker.rs`` file, the ``events/mod.rs`` file, and the ``events/<Name_of_Event_Here>.rs`` files.

## events/<Name_of_Event_Here>.rs File
These files are special because they can be called ehatever you'd like your event name to be. These files are also the most complex as they will contain any logic you'd like to trigger when the custom event is recieved. Here is an example at ``event/test.rs``

```RUST
///////////////////////////////
//   A sample custom event   //
///////////////////////////////

pub fn main () {
    println!("Got test custom event");
}
```

## mod.rs File

The mod.rs file allows linker.rs to detect our custom event file and feed it to the compiler when needed. here is ours for our ``test.rs`` custom event:

```RUST
// Register Custom Events

pub mod test;
```

## Event Linker File
The next file you need to set up is ``linker.rs``. It's job is to link the events we defined in ``events/mod.rs`` and link them to a socket event. Here is what the ``linker.rs`` file would look like with our custom event:

```RUST
mod events;

////////////////////////////////////////////////////////
// Register some custom events with our socket server //
// Your custom events will also be registered here as //
// well as in the ./events/mod.rs file.               //
////////////////////////////////////////////////////////

socket.on(
    "test",
    move || {
        test::main();
    },
);

```