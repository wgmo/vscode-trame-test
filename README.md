# Demonstrate VSCode PyVista notebook failure

A distilled example of something from our codebase which used to work, and at
some point recently stopped.

## Run using Jupyter

Launch the notebook in Jupyter to see that it works fine there:

```shell
 uv run jupyter notebook test-pyvista-trame.ipynb
 ```

This will launch the browser 

If you run the only cell, you'll see the pyvista interactive plot appears
happily (there's nothing in it of course!)

## Run using VSCode

Try running the same cell in VSCode, the error is produced:

```
usage: ipykernel_launcher.py [-h] [--server] [--banner] [--app] [--no-http]
                             [--authKeyFile AUTHKEYFILE] [--hot-reload]
                             [--trame-args TRAME_ARGS] [--follow-symlinks]
                             [--debug] [--nosignalhandlers] [--host HOST]
                             [-p PORT] [--timeout TIMEOUT] [--content CONTENT]
                             [--authKey AUTHKEY] [--ws-endpoint WS]
                             [--no-ws-endpoint] [--fs-endpoints FSENDPOINTS]
                             [--reverse-url REVERSE_URL] [--ssl SSL]
ipykernel_launcher.py: error: ambiguous option: --f=/mnt/wslg/runtime-dir/jupyter/runtime/kernel-v38d295f21f4362e54e6cfaddca49cdc13964b1eb0.json could match --follow-symlinks, --fs-endpoints
```

```
An exception has occurred, use %tb to see the full traceback.

SystemExit: 2
```

Note that this happens on the call to `plotter.show()`.

Something in the way trame interacts with VSCode to attempt to launch the
client-server communication is causing this issue. Reading around, the `-f`
option appears outdated. Quick exploration did not find me where in VSCode this
call is made.