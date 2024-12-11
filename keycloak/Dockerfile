# Используем официальный образ Keycloak
FROM quay.io/keycloak/keycloak:25.0.2

USER root

# Копируем скомпилированный jar-файл в директорию провайдеров Keycloak
COPY ./*.jar /opt/keycloak/providers

# Устанавливаем владельца и права доступа для Keycloak
RUN chown -R 1000:1000 /opt/keycloak/providers/*.jar

# Переключаемся обратно на пользователя Keycloak
USER 1000

ENV KEYCLOAK_ADMIN=admin
ENV KEYCLOAK_ADMIN_PASSWORD=admin

ENV KC_DB=postgres
ENV KC_DB_URL=jdbc:postgresql://postgres:5432/kwagga
ENV KC_DB_SCHEMA=keycloak
ENV KC_DB_USERNAME=postgres
ENV KC_DB_PASSWORD=Rustam2003
ENV KC_HOSTNAME=id.kwagga.ru

RUN /opt/keycloak/bin/kc.sh build

# Запускаем Keycloak
ENTRYPOINT ["/opt/keycloak/bin/kc.sh", "start-dev", "--log-level=DEBUG", "--https-port=8443", "--hostname=https://id.kwagga.ru"]