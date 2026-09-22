# ts_modeling

```mermaid
# scripts/generate_roadmap_svg.jl
using Graphviz_jll

dot_script = """
digraph Roadmap {
    // Canvas & Layout Settings
    graph [
        rankdir=TB,
        pad="0.5",
        nodesep="0.5",
        ranksep="0.6",
        bgcolor="transparent",
        fontname="Helvetica,Arial,sans-serif"
    ];

    // Default Node Formatting (Fixes text clipping & ugly square borders)
    node [
        shape=rect,
        style="filled,rounded",
        fontname="Helvetica,Arial,sans-serif",
        fontsize=12,
        penwidth=0,
        margin="0.3,0.15",  // <--- Extends padding around text to stop clipping
        width=0,
        height=0
    ];

    // Default Edge/Arrow Formatting
    edge [
        color="#8b949e",
        penwidth=1.5,
        arrowsize=0.8
    ];

    // Node Categories (GitHub Color Palette)
    // Done (Green)
    node [fillcolor="#2da44e", fontcolor="#ffffff"];
    S2 [label="§2. Public API Contract"];

    // In Progress (Blue)
    node [fillcolor="#0969da", fontcolor="#ffffff"];
    S1 [label="§1. Geometry & Mesh Validation"];
    S6 [label="§6. Fourier Matching Envelope"];

    // In Queue (Muted Gray)
    node [fillcolor="#6e7781", fontcolor="#ffffff"];
    S3 [label="§3. Nonzero-loss VESM"];
    S5 [label="§5. Arbitrary Shapes & Registered Fish"];
    S4 [label="§4. Solver Reliability"];

    // Dependency Connections
    S1 -> S5;
    S3 -> S5;
    S6 -> S4;
}
"""

# Render SVG
dot_exe = Graphviz_jll.dot()
open(`$dot_exe -Tsvg -o docs/src/assets/roadmap.svg`, "w") do io
    print(io, dot_script)
end
```
