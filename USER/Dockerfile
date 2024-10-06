FROM almalinux:9
RUN adduser -D expense
# The adduser -D expense command creates a new user named expense without a password.
USER expense
CMD ["tail", "-f", "/dev/null"]