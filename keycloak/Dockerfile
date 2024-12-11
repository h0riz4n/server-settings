# Используем официальный образ Keycloak
FROM quay.io/keycloak/keycloak:25.0.2

USER root

# Копируем скомпилированный jar-файл в директорию провайдеров Keycloak
COPY ./*.jar /opt/keycloak/providers

# Устанавливаем владельца и права доступа для Keycloak
RUN chown -R 1000:1000 /opt/keycloak/providers/*.jar

COPY ./domain_name.pem /app/cert/domain_name.pem
COPY ./key.pem /app/cert/private.pem

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
# ENV KC_HTTPS_CERTIFICATE_FILE=/app/cert/domain_name.pem
# ENV KC_HTTPS_CERTIFICATE_KEY_FILE=/app/cert/private.pem

RUN /opt/keycloak/bin/kc.sh build

# Запускаем Keycloak
ENTRYPOINT ["/opt/keycloak/bin/kc.sh", "start-dev", "--log-level=DEBUG", "--hostname=https://id.kwagga.ru"]