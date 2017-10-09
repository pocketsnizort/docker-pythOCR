# docker-pythOCR
a docker version of [pythocr](https://github.com/pocketsnizort/pythOCR) python OCR script


How to use
==========

Like the original script, but because it is dockerized, you need to mount some stuff, here is an exemple:

```
docker run --rm -it \
-v /path/to/my/vpys:/vpys:ro \
-v /path/to/my/input/dir:/input:ro \
-v /path/to/my/output/dir:/output \
-v /path/to/my/config:/userconfig:ro \
pythocr --mode ful -c /userconfig/my-conf.ini --timid --vpy /vpys/my-vpy.vpy /input/my-video.mp4
```

Some explaination:
- `--rm` to delete the container after it has finished, because this container is more of a "launched manually" than a real service. It will NOT delete the data present in you mounted volumes.
- `-it` Necessary if you use the `--timid` option as it requires user input.
- `-v /path/to/my/vpys:/vpys:ro` mount folder containing vapoursynth scripts necessary to the filtering job (may be omited in cas of `--mode ocr`). the `ro` stands for read-only.
- `-v /path/to/my/input/dir:/input:ro` mount of input folder, note that you can mount a file directly so in the command above, we could just use `-v /path/to/my/input/dir/my-video.mp4:/input/my-video.mp4:ro`
- `-v /path/to/my/output/dir:/output` mount output folder, do not forget this one, and do not make it read-only.
- `-v /path/to/my/config:/userconfig:ro` mount of the configuration directory, there is no configuration included, so you may want to grab one [here](https://github.com/pocketsnizort/pythOCR/tree/master/config)