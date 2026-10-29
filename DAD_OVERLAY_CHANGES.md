# dad-overlay changes

This branch of iw4L is modified by the dad-rust project (2026). Upstream: vladtrc/iw4L at
acc57a5c9. The LICENSE (Apache 2.0) and NOTICE of upstream apply unchanged.

What changed, so a host application can draw its own world and lay iw4L's first-person view over it:

- `frame::ForeignCamera`: a marker for the host's own camera. iw4L's renderer, HUD and body
  presentation leave a camera with it alone. With no such camera, iw4L behaves as upstream.
- `render_scene::OverlayOnly`: a resource the host inserts (in the main and render apps) to draw
  only the first-person view, effects and models: the loaded map's world, static models and sky are
  not drawn, the camera clears to transparent, the full-screen post effects are skipped, and the
  load's GPU wait does not wait for map pipelines it will never draw.
- `render_gpu` render-frame diagnostics read a mesh's indices without panicking on meshes whose
  data lives only in the render world.
- `sim::equipment`: the grenade's launch velocity, fuse deadlines, fuse check, surface stick test,
  stick and unstick, and bounce are public, and `settle_stuck` (a sticking projectile settled on a
  face, without the landing spin and stick event) is split out of `settle_equipment`, which still
  calls it. A host that runs its own projectiles calls MW2's own grenade code.
