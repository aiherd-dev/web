# web.aiherd.dev

Build output. The dashboard bundle from the `aiherd` repo's `frontend/`,
published here as a static origin that serves **code only** — no user data, no
state, nothing per-user.

That separation is the point (`docs/remote-protocol.md` §11.8): a browser runs
whatever JavaScript its origin serves, so a dashboard shipped *through* a relay
would be a relay-chosen dashboard, and encrypting the transport underneath
attacker-supplied code protects nothing. This page reaches a herd only in
sealed `message/ohttp-*` blobs, with the pairing key arriving in a URL fragment
that never leaves the device.

Republish after a frontend change, from the `aiherd` checkout:

    ./build.sh web
    cp -R frontend/dist/. <this checkout>/ && git commit -am … && git push
