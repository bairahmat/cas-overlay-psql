CAS Overlay Template
============================

Generic CAS WAR overlay to exercise the latest versions of CAS. This overlay could be freely used as a starting template for local CAS war overlays. The CAS services management overlay is available [here](https://github.com/apereo/cas-services-management-overlay).

# Versions

```xml
<cas.version>5.0.x</cas.version>
```

# Requirements
* JDK 1.8+

# Configuration

The `etc` directory contains the configuration files and directories that need to be copied to `/etc/cas/config`.

# Build

To see what commands are available to the build script, run:

```bash
./build.sh help
```

To package the final web application, run:

```bash
./build.sh package
```

To update `SNAPSHOT` versions run:

```bash
./build.sh package -U
```
# Database
Install PostgreSql
- Create database `CREATE DATABASE CAS;` under cas user.
- Create table for authentication
```bash
CREATE TABLE public.users
(
  id integer NOT NULL,
  name text NOT NULL,
  email character varying(255),
  password character varying(255),
  CONSTRAINT users_pkey PRIMARY KEY (id)
)
```
- Insert dummy data username: user password: password
```bash
INSERT INTO users(id, name, email, password) values(1, 'test', 'user', '5f4dcc3b5aa765d61d8327deb882cf99');
```

# Configure CAS.PROPERTIES
cas-overlay-psql/etc/cas/config/cas.properties

# Deployment

- Create a keystore file `thekeystore` under `/etc/cas`. Use the password `changeit` for both the keystore and the key/certificate entries.
```bash
sudo keytool -genkey -alias tomcat -keystore /etc/cas/thekeystore -keyalg RSA -validity 365
```
- Ensure the keystore is loaded up with keys and certificates of the server.

On a successful deployment via the following methods, CAS will be available at:

* `http://cas.server.name:8080/cas`
* `https://cas.server.name:8443/cas`

## Executable WAR

Run the CAS web application as an executable WAR.

```bash
./build.sh run
```

## Spring Boot

Run the CAS web application as an executable WAR via Spring Boot. This is most useful during development and testing.

```bash
./build.sh bootrun
```

## External

Deploy resultant `target/cas.war`  to a servlet container of choice.

