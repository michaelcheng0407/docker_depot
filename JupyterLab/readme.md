## JupterLab docker image

### Packages installation
- Make sure pip-tools is installed. 
```
pip install pip-tools
```
- Specifies the python packages needed in the `requirements.in`. Run `pip-compile` to generate `requirements.txt`:

```
pip-compile requirements.in 
```

### JupyterLab configuration
- The `overrides.json` file allows customizing the default JupyterLab settings. This can be used to set the theme, behaviour, etc.

### Mount local notebooks folder 

In `docker-compose.yaml`, specify the local host folder containing your notebooks to bind into the container:

```yaml
volumes:
  - {notebooks folder}:/Python Notebook
``` 

### Build and starting the image
```
docker compose up -d
```

### Access the JupyterLab
- `http://localhost:8888`
- The default port is `8888`. It can be changed in the `docker-compose.yaml` file:
```yaml    
ports:
    - {external port number}:8888
```

