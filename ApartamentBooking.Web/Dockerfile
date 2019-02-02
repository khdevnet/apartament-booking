FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["SeatsBooking.Web/SeatsBooking.Web.csproj", "SeatsBooking.Web/"]
RUN dotnet restore "SeatsBooking.Web/SeatsBooking.Web.csproj"
COPY . .
WORKDIR "/src/SeatsBooking.Web"
RUN dotnet build "SeatsBooking.Web.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "SeatsBooking.Web.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SeatsBooking.Web.dll"]