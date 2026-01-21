# Question 1.

Understanding Docker images

Run docker with the python:3.13 image. Use an entrypoint bash to interact with the container.

What's the version of pip in the image?
1. 25.3
2. 24.3.1
3. 24.2.1
4. 23.3.1

## Answer

You can run `python:3.13` with `docker` and `interactive terminal` flag (`-it`)

```{bash}
docker run -it --rm -v $(pwd):/app python:3.13 pip -V
```

Result:
pip 25.3 from /usr/local/lib/python3.13/site-packages/pip (python 3.13)

so the answer is `25.3`

## Answer
>1. 25.3