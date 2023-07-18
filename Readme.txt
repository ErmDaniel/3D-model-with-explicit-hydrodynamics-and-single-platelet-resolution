#general description
This project describes the 3D dynamic particle-based model, which is able to analize mechanical properties of thrombus, and interplay between thrombus geometry, vessel geometry, thrombus porosity, and flow in vessel. 
Model is able to calculate hydrodynamic forces acting on thrombus, and flow velocities inside thrombus.  
Model uses Python, Numpy, Comsol Multiphysics software, and Mph project (https://mph.readthedocs.io/en/stable/installation.html).

#installation of modules
#use Pyhton 3.6-3.9 versions 
1. install numpy via 'pip install numpy'
2. install mph via 'pip install MPh'
3. you will need Comsol Multiphysics to run simulations

#usage example
#set input parameters
#set thrombus radius (in microns)
thrombus_radius=5
#set vessel radius (in microns)
vessel_radius=17
#set time of simulation (in ms)
time_simulation=20
#set extent of platelet activation
ext_act=0.35
#set thrombus porosity
input_porosity=0.7
#set path to design file (it is a Comsol file with .mph extension in project)
design_file='/home/user/design_file.mph'
#set path to output file
output_file='/home/user/output_file.mph'
#set path to directory where you want to store supplemental output data
dir_supplemental='/home/user/dir_supplemental_data'
#set path to directory where you want to store basic output data(output data will be stored in file dir_basic+'/r_'+str(thrombus_radius)+'_log'+'.txt')
dir_basic='/home/user/dir_basic_data'
#run simulation
#import module porous_thrombus_model.py
import porous_thrombus_model
#run simulation and get results
porous_thrombus_model.simulation(thrombus_radius,vessel_radius,time_simulation,ext_act,input_porosity,design_file,output_file,dir_supplemental,dir_basic)

#analisis of output results
#open file dir_basic+'/r_'+str(thrombus_radius)+'_log'+'.txt'
#content of lines

input data
V_thrombus- estimated thrombus volume after thrombus generation
input thrombus radius- thrombus radius
average platelet radius- average radius of platelet after thrombus generation
cylinder radius- vessel radius
time_simulation- time of simulation
ext_act- extent of platelet activation
number of platelets- number of platelets in thrombus

output data
number of interacting pairs of platelets- number of interacting pairs of platelets at the end of simulatuion

corrections to get proper mesh
number of corrected pairs of platelets- number of pairs of platelets to which radius correction procedure was applied
initial volume- sum of volumes of platelets before correction procedure
delta volume- difference between sum of volumes of platelets before and after correction procedure
delta percent- percentage difference  between sum of volumes of platelets before and after correction procedure

corrections near wall to get proper mesh
number of corrected platelets- number of pairs of platelets to which radius correction procedure was applied
initial volume- sum of volumes of platelets before correction procedure
delta volume- difference between sum of volumes of platelets before and after correction procedure
delta percent- percentage difference  between sum of volumes of platelets before and after correction procedure
output comsol data

real thrombus radius- real radius of thrombus after relaxation procedure
real thrombus-vessel contact radius- real radius of thrombus-vessel contact after relaxation procedure
internal radius- real thrombus radius - 4 microns 
deep radius-real thrombus radius/2
real thrombus-vessel contact area- area of contact between thrombus and vessel wall
z-projection of bulk hydrodynamic force- projection of sum of hydrodynamic forces acting on platelets on the direction of flow in vessel
contact force- platelet cross-section area* z-projection of bulk hydrodynamic force/real thrombus-vessel contact area
internal velocity- average flow z-velocity inside internal zone of thrombus
deep velocity- average flow z-velocity inside deep zone of thrombus
surface 2 layers velocity-  average flow z-velocity inside 2 surface layers of platelets in throbmus
internal porosity- porosity of the internal zone of thrombus
deep porosity- porosity of the deep zone of thrombus
inlet flow- flow in vessel
thrombus surface area- sum of surface areas of platelets in thrombus
average platelet radius- average radius of platelet in thrombus (based on thrombus surface area computation)
thrombus volume- volume of thrombus at the end of relaxation
surface-to-volume ratio- thrombus surface area/thrombus volume
time of computation in comsol- time of computation in Comsol Multiphysics 
time of computation- total time of computation
time of computation/n_platelets- total time of computation/number of platelets in thrombus