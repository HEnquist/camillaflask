# Backend server for CamillaGUI

This is the server part of CamillaGUI, a web-based GUI for CamillaDSP.

This version works with CamillaDSP 0.4.0 and up.

The complete GUI is made up of two parts:
- a frontend based on React: https://reactjs.org/ 
- a backend based on AIOHTTP: https://docs.aiohttp.org/en/stable/

## Setting up
### Python dependencies
Install the dependencies:
- python 3.6 or later
- websocket-client (required by pycamilladsp)
- aiohttp

For plotting, install these optional dependencies:
- numpy (required by pycamilladsp-plot)
- matplotlib (required by pycamilladsp-plot)



These are the names of the packages needed:
| Distribution | python | websocket-client | aiohttp | matplotlib | numpy |
|--------------|--------|------------------|-------|------------|---------|
| Fedora | python3 | python3-websocket-client | python3-aiohttp | python3-matplotlib | python3-numpy  |
| Debian/Raspbian | python3 | python3-websocket | python3-aiohttp | python3-matplotlib | python3-numpy |
| Arch | python | python-websocket-client | python-aiohttp | python-matplotlib | python-numpy |
| pip | - | websocket_client | aiohttp | matplotlib | numpy |
| Anaconda | - | websocket_client | aiohttp | matplotlib | numpy |

#### Linux
Most linux distributions have Python 3.6 or newer installed by default. Use the normal package manager to install the packages.

#### Windows
Use Anaconda: https://www.anaconda.com/products/individual. Then use Anaconda Navigator to install the dependencies.

#### macOS
On macOS use either Anaconda or Homebrew. The Anaconda procedure is the same as for Windows. 

For Homebrew, install Python with `brew install python`, after which you can install the needed packages with pip, `pip3 install websocket_client` etc.

### CamillaDSP Python libraries
For basic functionality you need:
- pycamilladsp from https://github.com/HEnquist/pycamilladsp

For plotting, you also need:
- pycamilladsp-plot from https://github.com/HEnquist/pycamilladsp-plot

To install a library first download it, either by `git clone` or by downloading a zip file of the code. Then unpack the files, go to the folder containing the `setup.py` file and run 
```sh
pip install .
```
Note that on some systems the command is `pip3` instead of `pip`.

If pycamilladsp-plot isn't installed, the plotting will be disabled. This makes it possible to run the backend on systems where matplotlib and/or numpy isn't available.

### Install gui server
Go to "Releases": https://github.com/HEnquist/camillagui-backend/releases
Download the zip-file ("camillagui.zip") for the latest release. This includes both the backend and the frontend.

Unzip the file, and edit `config/camillagui.yml` if needed.

```yaml
---
camilla_host: "0.0.0.0"
camilla_port: 1234
port: 5000
config_dir: "~/camilladsp/configs"
coeff_dir: "~/camilladsp/coeffs"
```
The included configuration has CamillaDSP running on the same machine as the backend, with the websocket server enabled at port 1234. The web interface will be served on port 5000. It is possible to run the gui and CamillaDSP on different machines, just point the `camilla_host` to the right address.

The settings for config_dir and coeff_dir point to two folders where the backend has permissions to write files. This is provided to enable uploading of coefficients and config files from the gui. 


## Running
Start the server with:
```sh
python main.py
```

The gui should now be available at: http://localhost:5000/gui/index.html

If accessing the gui from a different machine, replace "localhost" by the IP or hostname of the machine running the gui server.


