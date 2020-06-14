# Calculator of Type _D_ structures and knot Floer homology for three strand pretzel knots

* The following is written by Daniel Waite, during the study for his Ph.D. in mathematics at the University of Glasgow.
* The code is an adaptation of code written by P. Ozsvath and Z. Szabo, found at the link below, which calculates their algebraic knot invariant recently proven to be equivalent to classical knot Floer homology. 
 ** https://web.math.princeton.edu/~szabo/HFKcalc.html
* This is specifically written for the calculation of this bordered invariant for three-strand pretzel knots, and the extraction of Type _D_ structures at any intermediate point in their algorithm.
* Unlike Ozsvath-Szabo's original code, the Morse Diagram for which the invariants are to be calculated must be procided, rather than a determination of the Morse diagram from a PD-code.
* Since this code is written for the purpose of computations for three strand pretzel knots, the girth of the diagram is hard-coded.
* There is a Python wrapper to produce the relevant Morse diagram for any three-strand pretzel knot of the form _P(2c+1,-2b-1,2a)_, where a,b and c are natural numbers.

# Requirements.

* For compilation, g++/gcc is currently used in the compilation script _CompileCalculator.sh_, using C++11.
* The python wrapper is Python 3, but requires no other prerequisites.

# Building and running the executable

* Download all files in the repository, including the empty file Output
* Run the compilation shell script _CompileCalculator.sh_. Any errors should be flagged.
* The script should generate an executable computeFromMorseFile.run 
  ** Run wit ./computeFromMorseFile.run MorseFile Stage SimplifyBool
  ** To run, this script takes three arguments.
    *** MorseFile : The string containing the path to the file with the Morse code for the knot.
    *** Stage : Natural number, denoting the point in the Morse Diagram at which the Type _D_ structure should be extracted.
    *** SimplifyBool: Integer. If 0, no simplification of the Type _D_ structure occurs until after the required stage for Type _D_ structure extraction. Else, this simplification of the Type _D_ structure occurs at every point.
   ** MorseFile should contain the valid, girth 6 MorseDiagram for a knot, such that every minimum is placed between strands 1 and 2. No check is made that this is a valid knot, but errors and faults will occur if a knot is not specified.
    *** 1000 X denotes a left to right maximum where the leftmost strand of the new maximum is the X-th strand.
    *** 1001 X denotes a right to left maximum where the leftmost strand of the new maximum is the X-th strand.
    *** K if positive denots a positive crossing between strands K and K+1. If negative, a negative crossing between these strands
    *** -1000, a minimum between the first and second strands.
 * A python exectuable ./Pretzel_Run.py to wrap the generation of a Morse Diagram and running of the executable to generate the ranks of the groups equivalent to the hat-version of knot Floer homology, and associated concordance invariants.
  ** Run this as ./PretzelRun.py $A $B $C
  ** This will return to std_out the result from _./computeFromMorseFile.run Morse_Knot_Form LARGE 0_ , where LARGE is a large integer.
* When running the executable _computeFromMorseFile.run_, if Stage is specified, the arrows and generators of the Type _D_ structure at i=Stage are provided in two files. ./Output/Generators and ./Output/Arrows.
  ** Generators contains a list of generators. The first value is the label, the second the associated idempotent, the third the Maslov grading and the fourth the Alexander grading.
  ** Arrows contains a list of the maps in the Type _D_ structure. This contains triples A,B,M.
    *** A is the label of the generator at the start of the arrow.
    *** B is the label of the generator at the end of the arrow.
    *** M is the monomial part of the algebra element in the Type _D_ structure for the map from A to B.
