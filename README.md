# Data models and scripting languages for field-agent based modelling

This repository holds a Jupyter notebook demonstrating the Daisyworld model implementation in Campo,
a YAML file to create the Python environment required to run the model,
and necessary scripts for pre- and postprocessing.

You can run the Jupyter notebook locally on your own computer.

More information will be given in the [GIScience 2023 workshop](https://campo.computationalgeography.org/workshops/giscience2023/).


## Running on your machine

### How to install

A few steps are required to run the Jupyter notebook.
General information on Jupyter notebooks and manuals can be found [here](https://jupyter.readthedocs.io/en/latest/).
The user guide and short reference on Conda can be found [here](https://docs.conda.io/projects/conda/en/latest/user-guide/cheatsheet.html).

 1. You will need a working Python environment, we recommend to install Miniconda. Follow their instructions given at:

    [https://docs.conda.io/en/latest/miniconda.html](https://docs.conda.io/en/latest/miniconda.html)

 2. Open a terminal (Linux/macOS) or Miniconda command prompt (Windows) and browse to a location where you want to store the course contents.

 3. Clone this repository, or download and uncompress the zip file. Afterwards change to the `giscience2023` folder.

 4. Create the required Python environment:

    Linux/macOS:

    `conda env create -f environment/environment.yaml`

    Windows:

    `conda env create -f environment\environment.yaml`


The environment file will create a environment named *giscience2023* using Python 3.11. In case you prefer a different name or Python version you need to edit the environment file.


### How to run

Activate the environment in the command prompt:

`conda activate giscience2023`

Then change to the `notebook` folder.
You can now start the Jupyter notebook from the command prompt. The notebook will open in your browser:

`jupyter lab daisyworld.ipynb`


## Running the LUE model

You can download the model script and input data [here](https://surfdrive.surf.nl/files/index.php/s/teEa1jAbmgsd6YG).
The model script can be executed e.g. with

`python ./model.py --hpx:threads=4 --write "50,50" input_path output_path`

For `output_path` create an output folder first, e.g. `output`
In case of crashes on Linux systems you can run like

`LD_PRELOAD=$(find $CONDA_PREFIX -name libtcmalloc_minimal.so.4) python ./model.py --hpx:threads=4 --write "50,50" input_path output_path`

### Output visualisation

You can display the output as raster timeseries with aguila. First, change the lines 224-225 in model.py into

```python
            self.write_raster(discharge, f"discharge_{timestep}.tif")
            self.write_raster(self.snow, f"snow_{timestep}.tif")
```

re-run the model and display the output with

`aguila --timesteps=[1,365] output/discharge`


## Further reading

Background on DaisyWorld:

  [https://en.wikipedia.org/wiki/Daisyworld](https://en.wikipedia.org/wiki/Daisyworld)

Scientific literature about Campo and LUE:

  M.P. de Bakker, K. de Jong, O. Schmitz, D. Karssenberg (2017). Design and demonstration of a data model to integrate agent-based and field-based modelling. Environmental Modelling & Software, 89, 172-189, DOI: [10.1016/j.envsoft.2016.11.016](https://doi.org/10.1016/j.envsoft.2016.11.016).

  K. de Jong, D. Karssenberg (2019). A physical data model for spatio-temporal objects. Environmental Modelling & Software, 122, 104553, DOI: [10.1016/j.envsoft.2019.104553](https://doi.org/10.1016/j.envsoft.2019.104553).

  K. de Jong, D. Panja, M. van Kreveld, D. Karssenberg (2021). An environmental modelling framework based on asynchronous many-tasks: Scalability and usability. Environmental Modelling & Software, 139, 104998, DOI: [10.1016/j.envsoft.2021.104998](https://doi.org/10.1016/j.envsoft.2021.104998).

[https://campo.computationalgeography.org/](https://campo.computationalgeography.org/)
