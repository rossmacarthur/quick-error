=============
Quick Error 2
=============

This is https://github.com/tailhook/quick-error but upgraded to Rust 2018 and support for
``Error::source()``. It has been published as ``quick-error2``. You can upgrade by updating your
``Cargo.toml`` to

.. code-block:: toml

    [dependencies]
    quick-error = { package = "quick-error2", version = "2" }

----
Why?
----

Because it seems like @tailhook is not currently maintaining ``quick-error``. Perhaps one day
https://github.com/tailhook/quick-error/pull/45 will be merged :man_shrugging:.

===========
Quick Error
===========

:Status: production-ready
:Documentation: http://tailhook.github.io/quick-error/

A macro which makes error types pleasant to write.

Features:

* Define enum type with arbitrary parameters
* Concise notation of ``Display`` and ``Error`` traits
* Full control of ``Display`` and ``Error`` trait implementation
* Any number of ``From`` traits
* Support for all enum-variants ``Unit``, ``Tuple`` and ``Struct``

Here is the comprehensive example:

.. code-block:: rust

    quick_error! {
        #[derive(Debug)]
        pub enum IoWrapper {
            Io(err: io::Error) {
                from()
                description("io error")
                display("I/O error: {}", err)
                cause(err)
            }
            Other(descr: &'static str) {
                description(descr)
                display("Error {}", descr)
            }
            IoAt { place: &'static str, err: io::Error } {
                cause(err)
                display(me) -> ("{} {}: {}", me.description(), place, err)
                description("io error at")
                from(s: String) -> {
                    place: "some string",
                    err: io::Error::new(io::ErrorKind::Other, s)
                }
            }
            Discard {
                from(&'static str)
            }
        }
    }

=======
License
=======

Licensed under either of

 * Apache License, Version 2.0, (./LICENSE-APACHE or http://www.apache.org/licenses/LICENSE-2.0)
 * MIT license (./LICENSE-MIT or http://opensource.org/licenses/MIT)

at your option.

------------
Contribution
------------

Unless you explicitly state otherwise, any contribution intentionally
submitted for inclusion in the work by you, as defined in the Apache-2.0
license, shall be dual licensed as above, without any additional terms or
conditions.
