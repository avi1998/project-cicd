# TODO

# We use .NET SDK version 6.0 for the build.

# Run the build scripts:
#  - src/web/restore.sh
#  - src/web/build.sh
#  you'll need to make the files executable first with chmod +x <filename>.


# Build output is in the folder:
#  /out

# The app should run using a .NET ASP.NET 6.0 image, with a minimal OS.
 
# We need to set four environment variables - 
# DOTNET_VERSION and APP_VERSION - for ops usage
# Widgetario__ProductsApi__Url set to "http://products-api/products"
# Widgetario__StockApi__Url set to "http://stock-api:8080/stock"

# The startup command needs to run the DLL from the build:
#  dotnet Widgetario.Web.dll
FROM mcr.microsoft.com/dotnet/sdk:6.0-alpine AS builder

WORKDIR /src
COPY src/web/ .

RUN chmod +x restore.sh && ./restore.sh
RUN chmod +x build.sh  && ./build.sh

# app image
FROM mcr.microsoft.com/dotnet/aspnet:6.0-alpine

ENV Widgetario__ProductsApi__Url="http://products-api/products" \
    Widgetario__StockApi__Url="http://stock-api:8080/stock" \
    DOTNET_VERSION="6.0" \
    APP_VERSION="1.0.0"

ENTRYPOINT ["dotnet", "/app/Widgetario.Web.dll"]

WORKDIR /app
COPY --from=builder /out/ .