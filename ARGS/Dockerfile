ARG version
FROM almalinux:${version:-8}
#RUN cat /etc/*release
ARG COURSE=Docker
ARG TRAINER=Balu Thripurari
ARG Duration=120HRS
ENV Duration=${Duration}
RUN echo "Course is: ${COURSE}, Trainer is: ${TRAINER}, Duration is: ${Duration}"
CMD [ "sleep","100" ]

#