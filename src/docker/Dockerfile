FROM httpd:alpine

# Remove any files that may be in the public htdocs directory already.
RUN rm -r /usr/local/apache2/htdocs/*

# Copy all the dontent of the build context into the htdocs directory
COPY . /usr/local/apache2/htdocs

# Remove the conf file from the htdocs directory, we need that in the conf directory instead
RUN rm /usr/local/apache2/htdocs/httpd.conf

# Specifically place the httpd config where it should be
COPY httpd.conf /usr/local/apache2/conf/httpd.conf


# Change owner of the publicly available files to root user and daemon group. Httpd threads run as daemon.
RUN chown -R root:daemon \
  /usr/local/apache2/htdocs/*

# Ensure that the files can only be read, even by the httpd server.
RUN chmod -R 440 \
  /usr/local/apache2/htdocs/*

# Make the files in the assets directory accessible
RUN chmod +x /usr/local/apache2/htdocs/assets
