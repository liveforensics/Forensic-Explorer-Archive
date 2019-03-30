# test for rabbitmq

FROM microsoft/dotnet-framework:4.7.2-runtime-windowsservercore-1803

# Metadata indicating an image maintainer
MAINTAINER @liveforensics

ENV ERLANG_HOME="c:\\erlang"
ARG RABBITMQ_VERSION=3.7.14
ENV RABBITMQ_VERSION=${RABBITMQ_VERSION}
ENV RABBITMQ_SERVER=C:\\rabbitmq_server-${RABBITMQ_VERSION}


RUN mkdir c:\\Temp
RUN mkdir c:\\erlang
ADD Wait-Service.ps1 /Wait-Service.ps1
ADD http://erlang.org/download/otp_win64_21.3.exe C:\\Temp\\erlang.exe
ADD https://github.com/rabbitmq/rabbitmq-server/releases/download/v3.7.14/rabbitmq-server-3.7.14.exe C:\\Temp\\rabbit.exe

RUN C:\\Temp\\erlang.exe /S /D="C:\\erlang"

RUN $path = [Environment]::GetEnvironmentVariable('Path', 'Machine'); \
    [Environment]::SetEnvironmentVariable('Path', $path + ';C:\\rabbitmq_server-' + $env:RABBITMQ_VERSION + '\\sbin', 'Machine')
RUN rabbitmq-plugins enable rabbitmq_management --offline

# RUN rmdir /S /Q c:\\Temp
CMD powershell.exe -file c:\Wait-Service.ps1 -ServiceName EventLog -AllowServiceRestart