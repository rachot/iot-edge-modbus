FROM arm32v7/gcc:7 AS build-env
WORKDIR /app

# copy .c and .h file
COPY src/*.c ./
COPY src/*.h ./

# build
RUN gcc -shared -o libcomWrapper.so -fPIC comWrapper.c

FROM microsoft/dotnet:2.0.0-runtime-stretch-arm32v7

ARG EXE_DIR=.

WORKDIR /app

COPY $EXE_DIR/ ./
COPY --from=build-env /app/libcomWrapper.so /usr/lib/

CMD ["/usr/bin/dotnet", "iot-edge-modbus.dll"]
