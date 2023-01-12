# AWS CloudFront React Serverless :cloud: :react: :serverless:

Este repositorio contiene un ejemplo de cómo configurar una aplicación React usando AWS CloudFront y AWS Lambda para un despliegue completamente serverless.

## CloudFront
[Amazon CloudFront](https://aws.amazon.com/cloudfront/) es una red de distribución de contenido (CDN) de AWS. Permite entregar contenido estático y dinámico a usuarios de todo el mundo con alta disponibilidad y escalabilidad.

## React
[React](https://reactjs.org/) es una librería JavaScript para construir interfaces de usuario. Es altamente escalable y se utiliza ampliamente en aplicaciones web y móviles.

## Serverless
[Serverless](https://www.serverless.com/) se refiere a la construcción y despliegue de aplicaciones y servicios sin la necesidad de provisionar y administrar servidores. AWS Lambda es una de las principales plataformas de serverless.

## Lambda
[AWS Lambda](https://aws.amazon.com/lambda/) es un servicio de computación en la nube que permite ejecutar código sin provisionar ni administrar servidores. Se utiliza para procesar eventos y automatizar tareas de back-end.

## serverless.yml


```` yml

CloudFrontDistribution:
      Type: AWS::CloudFront::Distribution
      Properties:
        DistributionConfig:
          Origins:
            - DomainName: ${self:custom.bucketName}.s3.amazonaws.com
              Id: ReactApp
              CustomOriginConfig:
                HTTPPort: 80
                HTTPSPort: 443
                OriginProtocolPolicy: https-only
          Enabled: true
          DefaultRootObject: index.html
          CustomErrorResponses:
            - ErrorCode: 404
              ResponseCode: 200
              ResponsePagePath: /index.html
          DefaultCacheBehavior:
            AllowedMethods:
              - DELETE
              - GET
              - HEAD
              - OPTIONS
              - PATCH
              - POST
              - PUT
            TargetOriginId: ReactApp
            ForwardedValues:
              QueryString: false
              Cookies:
                Forward: none
            ViewerProtocolPolicy: redirect-to-https
          ViewerCertificate:
            CloudFrontDefaultCertificate: true


````

* La propiedad DistributionConfig especifica la configuración para la distribución. Dentro de esta propiedad se especifica la configuración del origen de los recursos de la aplicación. 
* La propiedad Origins especifica una lista de orígenes de los recursos de la aplicación. En este caso, solo se especifica un origen. El origen se especifica mediante un objeto con las propiedades DomainName, Id y CustomOriginConfig.

* La propiedad DomainName especifica el nombre de dominio del origen de los recursos. En este caso, se está utilizando una variable de entorno personalizada llamada self:custom.bucketName que se refiere al nombre del bucket S3 en el que se encuentran los recursos de la aplicación.

* La propiedad Id especifica un identificador único para el origen. En este caso se le ha asignado el nombre ReactApp.

* La propiedad CustomOriginConfig especifica la configuración de origen personalizado. En este caso se especifican los puertos HTTP y HTTPS utilizados por el origen y se establece el protocolo de origen en https-only.


