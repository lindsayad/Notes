Whether the pressure is pinned or not, the velocity profile is identical. That's
a plus.

However, the profiles are different depending on whether the pressure is
integrated by parts or not.

So the oscillations are not caused by the convective term in the NS momentum
equation. It's definitely caused by the radial boundary condition at the axis of
symmetry.

Fantastic description of different classes of boundary conditions:
http://www.math.ttu.edu/~klong/Sundance/html/bcs.html

Well this is interesting; the _coord_type gets selected correctly when I run the
debug executable, but incorrectly when I run the opt executable.

I'm finding what Martin Leseur found: integrating p by parts creates
problems. Ok, there was a problem with the sign in the do nothing BC. When that
sign is fixed, the open flow problem is solved correctly in cartesian
coordinates whether the pressure is integrated by parts or not. The open flow
problem is solved correctly in cylindrical coordinates if the pressure is not
integrated by parts; but currently it does not converge to a solution if the
pressure is integrated by parts.

Tomorrow, record eigenvalue and flux values for different choices of the
postprocessor. Understand why the choice doesn't matter.

bxnorm = regular norm

+----------------+----------------+----------------+----------------+----------------+----------------+----------------+
| time           | bnorm          | eigenvalue     | group1max      | group1norm     | group2max      | group2norm     |
+----------------+----------------+----------------+----------------+----------------+----------------+----------------+
|   0.000000e+00 |   1.000000e+00 |   1.000000e+00 |   0.000000e+00 |   8.590069e+01 |   0.000000e+00 |   8.590069e+01 |
|   1.000000e+00 |   1.827927e+00 |   1.827927e+00 |   1.804033e-01 |   3.188402e+02 |   1.215683e-01 |   1.672426e+02 |
|   2.000000e+00 |   1.828075e+00 |   1.828075e+00 |   1.804071e-01 |   3.188541e+02 |   1.215784e-01 |   1.672560e+02 |
+----------------+----------------+----------------+----------------+----------------+----------------+----------------+

bxnorm = group1 norm

Postprocessor Values:
+----------------+----------------+----------------+----------------+----------------+----------------+----------------+
| time           | bnorm          | eigenvalue     | group1max      | group1norm     | group2max      | group2norm     |
+----------------+----------------+----------------+----------------+----------------+----------------+----------------+
|   0.000000e+00 |   1.164135e-02 |   1.000000e+00 |   0.000000e+00 |   1.000000e+00 |   0.000000e+00 |   1.000000e+00 |
|   1.000000e+00 |   1.049054e-02 |   1.828668e+00 |   1.034865e-03 |   1.828668e+00 |   6.967703e-04 |   9.598150e-01 |
|   2.000000e+00 |   1.048084e-02 |   1.828075e+00 |   1.034322e-03 |   1.828075e+00 |   6.970413e-04 |   9.589231e-01 |
+----------------+----------------+----------------+----------------+----------------+----------------+----------------+

bxnorm = group2 norm

Postprocessor Values:
+----------------+----------------+----------------+----------------+----------------+----------------+----------------+
| time           | bnorm          | eigenvalue     | group1max      | group1norm     | group2max      | group2norm     |
+----------------+----------------+----------------+----------------+----------------+----------------+----------------+
|   0.000000e+00 |   1.164135e-02 |   1.000000e+00 |   0.000000e+00 |   1.000000e+00 |   0.000000e+00 |   1.000000e+00 |
|   1.000000e+00 |   1.998091e-02 |   1.828113e+00 |   1.971931e-03 |   3.485134e+00 |   1.328793e-03 |   1.828113e+00 |
|   2.000000e+00 |   1.998051e-02 |   1.828075e+00 |   1.971815e-03 |   3.485013e+00 |   1.328828e-03 |   1.828075e+00 |
+----------------+----------------+----------------+----------------+----------------+----------------+----------------+

Notes on preconditioning:

asm-lu pre, full=false: linear its = 20
asm-lu pre, full=true: linear its = 17
default pre, full=true: linear its = 11
default pre, full=fase: linear its = 11
