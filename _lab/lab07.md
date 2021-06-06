---
layout: lab
num: lab07	
ready: true
desc: "Template Classes and Exceptions"
assigned: 2021-05-27
due: 2021-06-04 23:59
github_org_url: https://github.com/ucsb-cs32-s21
---

Goals
=====

Learning objectives. At the end of this lab, students should be able to:

- Add functionality to exisiting code base that draws 2D shapes (lecture project)
- Add to an exisiting class (representing an image) to make it templated (able to produce either .ppm, .pgm, .pbm or .txt, including practicing using template specialization)
- Introduce Exceptions to an exisitng code base to demonstrate handling odd behavior with grace

Orientation
============

As C++ is (mostly) a strongly typed language, however there are often computations we would like to apply to various types, templates give us the ability to apply general compute to a variey of types.  

In particular, we started this quarter with a lecture project that wrote out asci files to represent shapes (remember way back then).
![](asciFace.png)

At this point, we are creating drawings with color data:<br>
![](movablejpg.jpg)

However, we certainly can represent the same 'image' data as either a character (asci), black and white (boolean), greyscale (integer) or color (r, g, b).  Our first goal for this lab is to use templates to support these varous output types for our drawing program.

The next big idea we are playing with is that many times when our program is running things can go wrong.  We can use assert and debugging and hope our user (and other software engineers) will be well behaved, however, we can also plan to have our programs fail gracefully if all else fails.  We will do this using exceptions.  Exception design is an art that we will only just start to experiment with.  The second half of this lab involves adding exception handling for when unexpected issues arise in the drawing program.


Modality
============
This is a pair lab.  You may choose to work alone or with another student.  When working in a pair, please always follow good pair programming methodologies.  In general, set aside time to work together and share your screen to share the work and learning.  

You will need to identify you partner (pair) in your submission (add a header to your main with both your names!).  For this lab, you *MAY* partner with anyone (i.e. even someone you paired with twice before) as it is a different code base (lecture code).

Task 1
============

Download the base code.  It is a version of our lecture code with a class to write out a color image (as we have been doing) - see image.h.
https://github.com/ucsb-cs32-s21/lab07-STARTER

You need to modify this class so that it is templated in terms of the type that the image stores.  Change all methods that operate on a 'color' to instead work on a templated type.

As we will need some methods to vary for the different types, use template specialization for the following methods (only):
```
writeHeader
writePixel
```
For the header information, see: http://paulbourke.net/dataformats/ppm/
for an example of the difference in the header for the different image types (PPM, PGM, PBM).

Modify createImage.h (then you can use TestmainPartial.cpp as your main once you uncomment the code - this would then completely replace main.cpp). You will also need to use template specialization in createImage.h for:
```
void createImage
```
in order to set the templated values in the image.  In general, for a color image, use the colors returned by specific shapes, for a greyscale image, use the scaled brightness of the shape's color to set the greyscale value, for a black and white image and an asci image use the value of 'inC' as the interior value.

The tests that the autograder will run are shown in TestmainPartial.cpp, but in genernal, make sure you can output all four image types: color, greyscale, black and white and asci (only partial image shown below due to size!). These outputs were produced with ./a.out 200 200 out

![](outPPM.jpg)
![](outPGM.jpg)
![](outPBM.jpg)
![](partialAsci.png)

Task 2
============
Next, we will add some exception handling to the code. Mostly our goal is to create a drawing if we can, even if the user makes an error in their specification.
We will use exceptions to try to catch and warn about issues but also proceed with drawing as best we can.

First be sure you have the most recent version of polygon.h/cpp as it has a useful helper function.  In general, you need to add a step prior to drawing which
validates whether all shapes can be drawn as expected.  Add a pure virtual method to shape called
```
validate
```
and before creating an image, validate that all shapes are drawable. (The example TestmainPartial.cpp file includes an example).
```
		//prior to creating image test all valid
		for (auto s : theShapes) {
			s->validate();
		}
```

For each concrete class, use try and catch (potentially nested - consider your design) such that the following is true:<br>
1) If an ellipse has a center vertex with a value less than zero, a warning is printed ("ellipse center less zero") and the color of the ellipse is changed to black<br>
2) If an ellipse has either radius specified as zero (such that evaluate function will have a divide by zero exception), warn ("ellipse divide zero") and change the zero valued radius to 2 and color the ellipse red.<br>
3) If a rectangle has any of its vertices with values less than zero,  a warning is printed ("rect vert less zero") and the color of the rectangle is changed to black<br>
4) If a rectangle is created with its vertices out of order (i.e. first vertex is not upper left values), a warning is printed ("rect order incorrect"), the vertices are correctly ordered (for proper drawing) and color the rectangle red.<br>
5) If a polygon has any of its vertices with values less than zero,  a warning is printed ("polygon vert less zero") and the color of the polygon is changed to black<br>
6) If a polygon is concave, our drawing method will fail (as is*), thus, print a warning ("polygon concave"), change the polygon to be a triangle formed by the first, second and final vertex and color the polygon red. (Note a helper function to detect concave polygons is provided in the new code, make sure you have it<br>

**A red re-coloring has priority**. Note, this implies an ordering on the warnings as well.<br>
For the exceptions - think about using some of the standard exceptions - for example, std::out_of_range or std::domain_error.

A partial example main.cpp (called TestmainPartial.cpp) is provided demonstrating the testing we expect your code to support.

*Note that the general approach to handle concave polygons is to turn it into a set triangles.  We will skip the full solution for this lab and only create one triangle.

The example partial main includes the following shapes:
```
	/* four polygons - 2 concave */
	vector<vec2> Verts0;
	Verts0.push_back(vec2(50, 50));
	Verts0.push_back(vec2(75, 25));
	Verts0.push_back(vec2(100, 50));
	Verts0.push_back(vec2(100, 100));
	Verts0.push_back(vec2(50, 100));
	shared_ptr<Polygon> t2 = make_shared<Polygon>(Verts0, 5, color(250)) ;

	vector<vec2> Verts1;
	Verts1.push_back(vec2(200, 50));
	Verts1.push_back(vec2(225, 75));
	Verts1.push_back(vec2(250, 50));
	Verts1.push_back(vec2(250, 100));
	Verts1.push_back(vec2(200, 100));
	shared_ptr<Polygon> t3 = make_shared<Polygon>(Verts1, 5, color(250)) ;

	vector<vec2> Verts2;
	Verts2.push_back(vec2(50, 200));
	Verts2.push_back(vec2(100, 200));
	Verts2.push_back(vec2(100, 250));
	Verts2.push_back(vec2(50, 250));
	shared_ptr<Polygon> t4 = make_shared<Polygon>(Verts2, 5, color(250)) ;

	vector<vec2> Verts3;
	Verts3.push_back(vec2(200, 200));
	Verts3.push_back(vec2(210, 240));
	Verts3.push_back(vec2(250, 250));
	Verts3.push_back(vec2(200, 250));
	shared_ptr<Polygon> t5 = make_shared<Polygon>(Verts3, 5, color(250)) ;


	theShapes.push_back(t2);
	theShapes.push_back(t3);
	theShapes.push_back(t4);
	theShapes.push_back(t5);
	
	/*ellipse with zero divisor*/
	theShapes.push_back(make_shared<ellipse>(vec2(150, 150), 0, 0, 14, color(250)));	
	
	//rect with reversed corners
	theShapes.push_back(make_shared<Rect>(vec2(170, 80), vec2(120, 60), color(250), 8));

	/*polygon out of bounds */
	vector<vec2> Verts4;
	Verts4.push_back(vec2(-10, 150));
	Verts4.push_back(vec2(10, 130));
	Verts4.push_back(vec2(10, 170));
	shared_ptr<Polygon> t6 = make_shared<Polygon>(Verts4, 5, color(250)) ;
	theShapes.push_back(t6);

	/*ellipse out of bounds*/
	theShapes.push_back(make_shared<ellipse>(vec2(150, -2), 4, 28, 14, color(250)));	

	//rect out of bounds and inverted vertices */
	theShapes.push_back(make_shared<Rect>(vec2(10, 210), vec2(-10, 240), color(250), 4));

	/*ellipse out of bounds and zero radius! */
	theShapes.push_back(make_shared<ellipse>(vec2(-2, 50), 40, 0, 14, color(250)));		

	/*polygon out of bounds  and concave!*/
	vector<vec2> Verts5;
	Verts5.push_back(vec2(-10, 250));
	Verts5.push_back(vec2(50, 290));
	Verts5.push_back(vec2(140, 300));
	Verts5.push_back(vec2(-10, 300));
	shared_ptr<Polygon> t7 = make_shared<Polygon>(Verts5, 5, color(250)) ;
	theShapes.push_back(t7);

  ```
  
Expected output for the example TestmainPartial is:<br>
![](fix.jpg)

The tex output for the errors for the above TestmainPartial would be:
```
polygon concave
polygon concave
ellipse divide zero
rect order incorrect
polygon vert less zero
ellipse center less zero
rect vert less zero
rect order incorrect
ellipse center less zero
ellipse divide zero
polygon vert less zero
polygon concave
writing an image of size: 300 300 to: out
```
-------

Grading:<br>
(60) autograders (correct run with images of various types and correct run with shapes specified with errors)<br>
(40) code review (offline not in person) evaluating correct visual output for the poorly specified shapes and all templated image output files correct<br>

