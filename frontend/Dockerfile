# syntax=docker/dockerfile:1

FROM httpd:2.4

# Install git
RUN apt-get -y update
RUN apt-get -y install git

# Configure apache
COPY httpd.conf /usr/local/apache2/conf/httpd.conf
COPY web.conf /usr/local/apache2/conf/sites/vnint.conf

# Clone the Vnint repository
RUN git clone https://github.com/C0mput3r5c13nt15t/Vnint.git Vnint

# Copy the www folder to the right location
RUN cp -r ./Vnint/www/* /usr/local/apache2/htdocs/
