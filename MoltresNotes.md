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
