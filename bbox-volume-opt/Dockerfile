# build:
#       docker build -t ext_volume/opt .
# run:
#       docker run -it --name opt_for_XXX ext_volume/opt /bin/sh (and exit, noreq up)
# use:
# !!! image must have "/opt/" !!!
#       docker run -it --rm --volumes-from opt_for_XXX centos:centos6 bash
# backup:
#       docker run -t  --rm --volumes-from opt_for_XXX -v $(pwd):/BACKUP busybox sh -c "tar cv -C / opt | gzip -c > /BACKUP/opt.tar.gz"

FROM   busybox
VOLUME ["/opt"]
CMD    ["/bin/sh", "-c", "watch -n 5 df -h -P"]
