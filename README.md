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

    VITE_GIT_VERSION=$(git describe --tags) ./build.sh web
    cp -R frontend/dist/. <this checkout>/
    git rm --cached <the previous assets/index-*.js and .css> && git add -A
    git commit && git push

`cp -R` merges, so the previous hashed bundle stays behind unless it is
removed by hand. Set `VITE_GIT_VERSION` yourself: only `cargo build` sets it,
and `./build.sh web` alone leaves the footer version blank.

`docs/web-aiherd-dev.md` in the `aiherd` repo has the rest — DNS, the reload
that used to fire on every fresh tab, and where the favicon comes from.
