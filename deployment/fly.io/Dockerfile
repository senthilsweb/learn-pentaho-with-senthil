ARG TAG=22.04
FROM ubuntu:${TAG}


# Install maven, wget, unzip & sudo
RUN apt-get update && apt-get install wget unzip sudo openjdk-17-jdk maven -y \
    && rm -rf /var/lib/apt/lists/*

# Create devuser and add to sudoers
RUN useradd -m -s /bin/bash devuser \
    && echo 'devuser:pentaho' | chpasswd \
    && usermod -aG sudo devuser \
    && mkdir -p /home/devuser/pentaho/design-tools \
    && mkdir -p /home/devuser/.kettle \
    && mkdir -p /home/devuser/.pentaho/metastore


COPY ./pdi-ce-10.2.0.0-222/data-integration /home/devuser/pentaho/design-tools/data-integration   
COPY ./setups/config-files/carte.xml /home/devuser/pentaho/design-tools/data-integration/
COPY ./setups/config-files/repositories.xml /home/devuser/pentaho/design-tools/data-integration/
COPY ./setups/jdbc-drivers/*.* /home/devuser/pentaho/design-tools/data-integration/lib/
COPY ./setups/config-files/metastore /home/devuser/.pentaho/metastore
COPY ./jobs /home/devuser/pentaho/design-tools/data-integration/jobs


# Set working directory
WORKDIR /home/devuser/pentaho/design-tools/data-integration

# Expose port
EXPOSE 5000

# Command to run
CMD ["./carte.sh", "0.0.0.0", "5000"]