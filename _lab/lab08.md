---
layout: lab
num: lab08	
ready: false
desc: "Exceptions and Template Classes"
assigned: 2021-03-03
due: 2021-03-10 23:59
github_org_url: https://github.com/ucsb-cs32-w21
---

Goals
=====

Learning objectives. At the end of this lab, students should be able to:

- Add functionality to exisiting code base that draws 2D shapes (lecture project)
- Introduce Exceptions to an exisitng code base to demonstrate handling odd behavior with grace
- Add to an exisiting class (representing an image) to make it templated (able to produce either .ppm, .pgm, .pbm or .txt, including template specialization

Orientation
============

As C++ is (mostly) a strongly typed language, however there are often computations we would like to apply to various types, templates give us the ability to apply general compute to a variey of types.  

In particular, we started this quarter with a lecture project that wrote out asci files to represent shapes (remember way back then).

