# pineal

> Backend-agnostic visualization — the "third eye". A catalog of GPU painters over a single `Canvas` trait, in Rust, on [Llimphi](https://gitea.gioser.net/sergio/llimphi).

`pineal` is a catalog of specialized painters — cartesian, polar, mesh, treemap, phosphor, flow, heatmap, stream, financial, hexbin, contour, bars — over **one painter abstraction**, the `Canvas` trait. Any program can push shapes to a pineal and get pixels without carrying its own graphics stack. The whole chain `core → render → painter` is **agnostic of the backend**: the same painter draws to vello/Llimphi on screen, to software PNG/SVG/PDF offline, or straight to the GPU for millions of primitives.

pineal **does not compute — it only draws.** Simulation lives elsewhere; pineal turns the output into pixels. It's the hammer, not the carpenter.

## Quick start — the gallery

```sh
cargo run --release -p pineal-galeria-demo   # 11 painters tiled in one window
cargo run --release -p pineal-gpu-demo       # 3D starfield, up to 1M primitives/frame (D = density, space = pause)
```

Each painter also has its own demo: `pineal-{heatmap,hexbin,treemap,mesh,financial,flow,contour,bars,polar,phosphor,stream}-demo`.

## Crates

`pineal-core` (agnostic primitives: interleaved DataBuffer, streaming RingBuffer, SpatialIndex, LTTB, scales — zero UI deps, zero alloc in the hot path) · `pineal-render` · one crate per painter · `pineal` (umbrella re-export for prototyping; in production import the leaf crates so tree-shaking drops the unused).

## How dependencies work

This is a clean, light front-door: pineal's only external dependency is the [Llimphi](https://gitea.gioser.net/sergio/llimphi) UI framework, pulled as a git dependency. No monorepo clone, no vendoring — `pineal-core`/`render` are backend-agnostic and the on-screen path is the only one that touches Llimphi.

## License

MIT. Builds on [Llimphi](https://gitea.gioser.net/sergio/llimphi).
