# GopFramebuffer

UEFI GOP framebuffer and MobileFramebuffer integration.

CPU and GPU scanout are supported. With `sheng-vsync=<Hz>`, a work-loop timer sends the MobileFramebuffer vsync message to the compositor.

Build and interface details: [documentation](https://unixnu.com/drivers/gop-framebuffer). Component sources and dependencies: [catalog](https://unixnu.com/reference/components).

## This fork

[FFT-infra/GopFramebuffer](https://github.com/FFT-infra/GopFramebuffer) is the
fork used by the Redmi K40 (`alioth`, SM8250-AC) port; the device repository
pins `b06fd74` on `main`.

Change over upstream:

- Republish the display service under the panel controller's name on request
  (`b06fd74`, the `dcls` experiment). Withdrawn on 2026-10-30: the sandbox
  refusal on the class name did not gate the wallpaper, and the service
  carried a name that is not upstream's.

The board drives scanout through this component with `offline-legacy-gop=1`
and `sheng-vsync=60`. `scripts/build-gop-legacy-display.py` in the device
repository archives the `late` library and re-proves its bindings to the
prelinked IOMobileFramebufferLegacy on every build.

Device page: <https://unixnu.com/zh/devices/alioth>.
Porting record: [`../UniXNU-alioth/porting.toml`](../UniXNU-alioth/porting.toml).

