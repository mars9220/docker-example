# Obspy Docker Image

In [run_ssh.sh](run_ssh.sh):

``` bash
docker container rm -f obspy_ssh
docker run -d \
        -p 49154:22 \
        -p 8888:8888 \
        -v /etc/passwd:/etc/passwd:ro \
        -v /etc/shadow:/etc/shadow:ro \
        -v /etc/group:/etc/group:ro \
        -v <path/to/workspace>:/home/${USER} \
        --name obspy_ssh obspy
```

1. Create a workspace directory.
2. Link `<path/to/workspace>` to the user home directory.
3. Change `49154` to any port for security.
4. Save and run `run_ssh.sh`.

If you want to start a Jupyter Lab server:

1. Paste [jupyter.sh](jupyter.sh) in to the workspace 
2. Run it and paste the url to the browser.

       http://127.0.0.1:8888/?token=36b31a373a9d18cc9b30a50883ad5a3638b19bed47be8074

3. Change the url IP if you run on a remote server. 