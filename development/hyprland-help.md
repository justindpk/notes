# Hyprland Helpful Tips/Commands

## Must Do's

Setting up fingerprint reader (allow user to be registered, default is root)

> sudo vim /etc/polkit-1/rules.d/49-fprintd.rules

> polkit.addRule(function(action, subject) {
>     if ((action.id == "net.reactivated.fprint.device.enroll" ||
>          action.id == "net.reactivated.fprint.device.verify" ||
>          action.id == "net.reactivated.fprint.device.delete") &&
>          subject.isInGroup("wheel")) {
>         return polkit.Result.YES;
>     }
> });

Upgrade / Update finger reader and other framework components

> fwupdmgr get-devices GUID
> fwupdmgr get-updates 1e8c8470-a49c-571a-82fd-19c9fa32b8c3
> fwupdmgr update GUID
