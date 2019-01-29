# Modeling Data
## Introduction
Based on [Open Cascade - Modeling Data](https://www.opencascade.com/doc/occt-7.2.0/overview/html/technical_overview.html#OCCT_TOVW_SECTION_3).

[Boundary representation](https://en.wikipedia.org/wiki/Boundary_representation) (BRep hereafter) is used to represent shapes in solid modeling.

In BRep the shape is represented as an aggregation of geometry within topology. The geometry is understood as a mathematical description of a shape, e.g. as curves and surfaces (simple or canonical, Bezier, NURBS, etc). The topology is a data structure binding geometrical objects together.

Geometry types and utilities provide geometric data structures and services for:
- Description of points, vectors, curves and surfaces:

  - their positioning in 3D space using axis or coordinate systems, and
  - their geometric transformation, by applying translations, rotations, symmetries, scaling transformations and combinations thereof.

- Creation of parametric curves and surfaces by interpolation and approximation;
- Algorithms of direct construction;
- Conversion of curves and surfaces to NURBS form;
- Computation of point coordinates on 2D and 3D curves;
- Calculation of extrema between geometric objects.

Topology defines relationships between simple geometric entities. A shape, which is a basic topological entity, can be divided into components (sub-shapes):

- Vertex – a zero-dimensional shape corresponding to a point;
- Edge – a shape corresponding to a curve and bounded by a vertex at each extremity;
- Wire – a sequence of edges connected by their vertices;
- Face – a part of a plane (in 2D) or a surface (in 3D) bounded by wires;
- Shell – a collection of faces connected by edges of their wire boundaries;
- Solid – a finite closed part of 3D space bounded by shells;
- Compound solid – a collection of solids connected by faces of their shell boundaries.

Complex shapes can be defined as assemblies of simpler entities.
