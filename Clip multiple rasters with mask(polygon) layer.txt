# Ensure that you have executed the code sequentially or copy it as a script

import os; import glob; import processing

# Define the path to the folder containing the shapefile and rasters
folder_path = 'C:/Users/gis/Desktop/Hidrocibalae_Final_task_20220128/Final QGis task/Data/'

# Define the path to the mask shapefile
mask_layer_path = os.path.join(folder_path, 'researchAreaBoundary.shp')

# Define the path to the folder containing the rasters
raster_folder = 'C:/Users/gis/Desktop/Hidrocibalae_Final_task_20220128/Final QGis task/Raster/'

# Get a list of all raster files in the folder
raster_files = glob.glob(os.path.join(raster_folder, '*.tif'))


# Iterate over the raster files
for raster_file in raster_files:
    # Construct the output file path for the clipped raster
    clipped_raster_path = os.path.join(raster_folder, 'clipped_' + os.path.basename(raster_file))
    
    # Define the algorithm parameters
    params = {
        'INPUT': raster_file,
        'MASK': mask_layer_path,
        'ALPHA_BAND': False,
        'CROP_TO_CUTLINE': True,
        'KEEP_RESOLUTION': False,
        'SET_RESOLUTION': False,
        'MULTITHREADING': False,
        'DATA_TYPE': 0,
        'OUTPUT': clipped_raster_path
    }

# Run the algorithm to clip the raster by mask
    processing.run('gdal:cliprasterbymasklayer', params)

    print(f'Raster {raster_file} clipped and saved as {clipped_raster_path}')


# Update the folder_path and raster_folder variables to the appropriate paths in your system.










