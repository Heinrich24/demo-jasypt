# DemoJasypt

## Description
The following will be a simple guide on how to encrypt sensitive information located in the application.properties file for a Java Spring Boot application.

## Encryption
For the encryption of sensitive information in the application.properties file you need to have the following (with the assumption that maven and java is installed and configured correctly):

- application.properties file
- pom.xml with the following plugin
```java
<plugin>
	<groupId>com.github.ulisesbocchio</groupId>
	<artifactId>jasypt-maven-plugin<artifactId>
	<version>3.0.3</version>
</plugin>
```

### Encryption Process
The steps that need to be followed to encrypt your sensitive information in the application.properties file.

- Define the values you would like to encrypt as follows in the application.properties file. The values you would like to encrypt needs to be place within the DEC() brackets. Please refer to the sample below where we will encrypt the value "MySenstiveInformationHere" with a encryption key.
```java
spring.password=DEC(MySenstiveInformationHere)
```
- Run the following command in the command line. Please replace the "dummyKey" with a unique password you would like to use to encrypt your DEC() values located within you application.properties file:
```cmd
mvn jasypt:encrypt -Djasypt.encryptor.password=dummyKey
```
- Upon successful execution your
```java
spring.password=DEC(MySenstiveInformationHere)
```
will change to
```java
spring.password=ENC(AgOVq/XinWM7YL9hi07XNkF3lDlexAzMOEb99wIv4prGtBaKrBIRuQEyVCHAMWH+)
```
The ENC() data contains the encrypted data. The data has now been encrypted with the Djasypt.encryptor.password specified during the mvn jasypt:encrypt process. 

## Running Java Application
Now that we have encrypted the sensistive values within application.properties file we need add the following argument when we wish to run our spring boot application:
- Command that will run your java application with the required password/key so that your application can utilize the encyrpted data.
```cmd
java -Djasypt.encryptor.password=dummyKey –jar yourapp.jar
```
Please note that you need to use the SAME password you initially used when encrypting the data during the encryption phase.


## Summary
You have now seen how you can encrypt senstive information located within the application.properties file. You have also been exposed on what arguments you need to pass through to your java application so that your application can read the encrypted data successefully.

## :thumbsup: Acknowledgement :fire:
I acknowledge that I do not soley own the right to the following code based and I give credit and acknowledgement to https://www.codejava.net/frameworks/spring-boot/spring-boot-password-encryption