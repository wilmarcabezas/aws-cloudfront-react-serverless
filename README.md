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



Para ver el código y configuración detallada, visita el [código fuente](https://github.com/wilmarcabezas/aws-cloudfront-react-serverless) :computer:


