# lab02-debugging

# Debugging Log
Link: https://www.shadertoy.com/view/wflfWf

mainImage:
- vec uv2 syntax error, should be vec2 uv
- raycast should use new uv2 instead of old uv
Found these out because shadertoy shows an error under syntax errors, but also because checking mainImage to me is the highest level before looking into more specific things.

raycast:
- H *= len * iResolution.x / iResolution.y (originally dividing by iResolution.x)
The spheres are all stretched so I assumed something would be going on with the SDF or raycast.  After checking raycast I located this bug.

march:
- Noticed that there simply wasn't enough floor, and there was a strange warping effect around the spheres and floor!!  So I looked at march and first increased the m value, and while this minorly helped it also had the effect of "expanding" everything being rendered, so I decided that probably wasn't the fix.  Then I realized that I could just increase the i bound to increase steps, so I increased it from 64 to 200 and that seems to have solved things!

sdf3D:
- From the current spheres and floor, clearly the reflection wasn't working, so I looked into the specular reflection calculation.  I wasn't sure where to look though so I enlisted the help of Niko, who then directed me to more closely scrutinize how the direction vector was being calculated.  I then realized that there is no point in using eye, since dir is the direction of the first ray.  I changed it to dir = reflect(dir, nor).

# Setup 

Create a [Shadertoy account](https://www.shadertoy.com/). Either fork this shadertoy, or create a new shadertoy and copy the code from the [Debugging Puzzle](https://www.shadertoy.com/view/flGfRc).

Let's practice debugging! We have a broken shader. It should produce output that looks like this:
[Unbelievably beautiful shader](https://user-images.githubusercontent.com/1758825/200729570-8e10a37a-345d-4aff-8eff-6baf54a32a40.webm)

It don't do that. Correct THREE of the FIVE bugs that are messing up the output. You are STRONGLY ENCOURAGED to work with a partner and pair program to force you to talk about your debugging thought process out loud.

Extra credit if you can find all FIVE bugs.

# Submission
- Create a pull request to this repository
- In the README, include the names of both your team members
- In the README, create a link to your shader toy solution with the bugs corrected
- In the README, describe each bug you found and include a sentence about HOW you found it.
- Make sure all three of your shadertoys are set to UNLISTED or PUBLIC (so we can see them!)
