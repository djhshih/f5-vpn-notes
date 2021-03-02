# F5 VPN connection notes

If your institution uses F5 VPN, it may enable two-factor authentication as well
as the endpint inspector, which must be installed on the client machine
(i.e. your computer).

Ironically, the endpoint inspector is poorly supported on client machines using
more secure operating systems (i.e. Linux distributions).

If your institution's VPN server does not require the endpoint inspector to run
on the client machine. You can simply login to the F5 VPN server in your web
browser, and that will be the end of it. Otherwise, you might be stuck wondering
how to install the endpoint inspector.

This guide walks through how to install the endpoint inspector on a Linux client
computer. Root access is required.

1. Login into the F5 VPN server via a web browser that uses
   `xdg-open` (e.g. Chrome).

2. You will be prompted to download the endpoint inspect.
   Download the `.deb` package.
   If you are on a x64_84 system, the packgage will be named
   `linux_f5vpn.x86_64.deb`.

3. Navigate to the package. Extract the `.deb` package with `ar`.

```
ar xv linux_f5vpn.x86_64.deb
```

You will now have two archives: `control.tar.gz` and `data.tar.gz`.

4. Install the content of `data.tar.gz` to `/opt`.

```
tar -xzvf data.tar.gz
sudo cp -r opt/f5 /opt/
```

5. Execute the post-installation script, which will register the
MIME type required to automatically start the F5 endpoint inspector
from the browser.

```
sudo sh postinst
```

6. Return to the browser and allow the endpoint inspector to execute when
when prompted with the `xdg-open` dialogue.

Now, you should be connected to the VPN network.

