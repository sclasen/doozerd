# Client API

This is just rough notes for now.

This is about the high-level interface exposed to application developers, not
the client protocol spoken between clients and servers on the wire.

I would encourage all junta client libraries in all languages to stick pretty
closely to this interface at a minimum. We'll try to design the wire protocol
so that that requirement isn't too onerous.

    Client() ==> c

    c.Get(path) ==> body, cas
    c.Set(path, body, cas) ==> cas
    c.ReadDir(path) ==> entries

    c.Lock(path, timeout) ==> ok
    c.Unlock(path) ==> ok

    c.AddCluster(uri)

Path example:

    /j/foo/wombat/pouch

Here, `foo` is a cluster name. Servers are initially discovered by DNS and
kept up to date by reading the junta keystore. Servers can also be explicitly
added by giving a `junta:` URI to the AddCluster method.

Cas tokens should be treated as opaque strings, though they are in fact
sequence numbers.