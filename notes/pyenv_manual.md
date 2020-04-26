## Install the pyenv
```bash
# Install pyenv for MAC
brew update
brew install pyenv
# Install pyenv for Ubuntu
# This should work, never tried myself.
curl https://pyenv.run | bash
```

##  Make a new Python version
```bash
#List all possible versions to install
pyenv install --list
#Install it
pyenv install 2.7.8
#create a virtual environment with the specific version
pyenv virtualenv 2.7.10 my-virtual-env-2.7.10
#List virtual environments present
pyenv virtualenvs
#Start using it
pyenv activate <name>
```

##  Delete an environment
```
pyenv uninstall my-virtual-env
pyenv virtualenv-delete my-virtual-env
```

##  Add python kernel to jupyterlab
```
#Create the environment if needed
virtualenv -p python3.6 py_36_env
# Activate it if needed
source py_36_env/bin/activate
pip install ipykernel
#install the kernel (ONLY IMPORTANT STEP)
python -m ipykernel install --user --name=py_36_env
jupyter notebook
```

#  Jupyter lab in remote server

1. First, connect to the server
    ```bash
    ssh user@server
    ```
2. Setup your password for notebook (jupyter lab access)
    ```bash
    jupyter notebook password
    #or
    jupyter lab --ip 0.0.0.0 --no-browser
    ```

3. Set notebook port and start without browser
    ```bash
    jupyter lab --port=9000 --no-browser &
    #or skip
    ```

4. Connect the server by creating a tunnel between running notebook on server and our machine
    ```bash
    ssh -N -f -L 8888:localhost:9000 user@server
    #or 
    ssh user@server -L 8888(localport):remote_ws:8888(remoteport)
    ```
        `-N` is for no remote process is run just connect ports.

        `-f` running the ssh background

        `-L` tells to forward out local (8888) to remote (9000) port

5. Go to localhost:8888 to access the notebook from local machine.

6. List notebooks running and close.
    ```bash
    jupyter notebook list
    #get pid and kill
    lsof -n -i4TCP:[port-number]
    kill -9 [PID]
    ```

##  Autosave .html and .py of notebooks
    ```bash
    #Generate the config:
    jupyter lab --generate-config
    ```
    Insert the code snippet below to config.
    ```bash
    import os
    from subprocess import check_call

    def post_save(model, os_path, contents_manager):
        """post-save hook for converting notebooks to .py and .html files."""
        if model['type'] != 'notebook':
            return # only do this for notebooks
        d, fname = os.path.split(os_path)
        check_call(['jupyter', 'nbconvert', '--to', 'script', fname], cwd=d)
        check_call(['jupyter', 'nbconvert', '--to', 'html', fname], cwd=d)

    c.FileContentsManager.post_save_hook = post_save
    ```
 
