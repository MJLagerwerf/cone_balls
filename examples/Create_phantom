
import numpy as np
import odl
# %%
def make_specs(center, radius, value=-1):
    rad = [radius, radius, radius]
    rot = [0, 0, 0]
    return [value, *rad, *center, *rot]

# %%
# Give the path where the specs of the foam sphere are saved
path = 'cone_foam_spec.txt'

ball_spec = np.loadtxt(path, dtype='float64')
ball_pos = ball_spec[:, :3]
ball_radius = ball_spec[:, 3]


# %% Create list of spheres
spheres = []
# Add outer sphere
spheres += [make_specs([0, 0, 0], .5, 1)]

# Add smaller spheres
for i in range(len(ball_radius)):
    spheres += [make_specs(ball_pos[i, :], ball_radius[i])]
    

# %% Create a reconstruction space
# Number of voxels in the x, y, and z direction
vox = 1024

# Physical size of the space
ph_size = 5

# Create space
reco_space = odl.uniform_discr(min_pt=[-ph_size, -ph_size, -ph_size],
                               max_pt=[ph_size, ph_size, ph_size],
                               shape= [vox, vox, vox])
# scaling factor to get the attenuation values realistic (this relates to ph_size)
scf = 0.24

# Create the foam phantom
phantom = odl.phantom.ellipsoid_phantom(reco_space, spheres) * scf

# %%
phantom.show()
phantom.show(coords=[None, 0, None])
phantom.show(coords=[0, None, None])


