FROM alpine:latest
COPY master-pdf-editor-4.3.89_qt5.amd64.tar.gz '/opt/'
COPY blank.pdf '/'
ARG tgz='master-pdf-editor-4.3.89_qt5.amd64.tar.gz'
ARG user='user'
RUN apk update && \
    apk upgrade && \
    apk add --no-cache \
        gcompat \
        libksane \
        qt5-qtbase \
        qt5-qtsvg \
        ttf-dejavu \
        msttcorefonts-installer && \
    echo "Fonts" && \
      update-ms-fonts && \
      fc-cache -f && \
      apk del msttcorefonts-installer && \
    echo "masterpdfeditor4" && \
      tar -xzf '/opt/master-pdf-editor-4.3.89_qt5.amd64.tar.gz' && \
      rm '/opt/master-pdf-editor-4.3.89_qt5.amd64.tar.gz' && \
      mv '/master-pdf-editor-4' '/opt/master-pdf-editor-4' && \
      ln -sf '/opt/master-pdf-editor-4/masterpdfeditor4' '/usr/bin/masterpdfeditor4' && \
    echo "Security / Unprivileged User" && \
      printf "" > /etc/securetty && \
      passwd -l root && \
      adduser -g "${user}" ${user} -s '/bin/sh' -D && \
      printf '%s:%s\n' "${user}" "$(od -vAn -N4 -tu4 < /dev/urandom)"  | chpasswd && \
    echo "Runtime" && \
      printf "export XDG_RUNTIME_DIR=/tmp/runtime-${user}\n" > "/etc/profile"
RUN \
    echo "Config" && \
      mkdir -p "/home/${user}/.config/Code Industry" && \
      printf "%s\n%s\n%s\n%s\n%s\n%s\n%s\n%s\n%s\n%s\n%s\n%s\n%s\n" \
             "[General]" \
             "app_style=Dark" \
             "check_updates=0" \
             "create_backup_file=false" \
             "enable_javascript=false" \
             "highlight_opacity=40" \
             "main-version=4389" \
             "parse_separate_all_forms=true" \
             "ImportFilePath=/home/${user}" \
             "openFilePath=/home/${user}" \
             "saveFilePath=/home/${user}" \
             "str_destination_save_as=/home/${user}" \
             > "/home/${user}/.config/Code Industry/Master PDF Editor.conf"
USER "${user}"
ENTRYPOINT [ "/bin/sh", "-lc", "masterpdfeditor4 blank.pdf" ]
# ENTRYPOINT [ "/usr/bin/masterpdfeditor4", "blank.pdf" ]
# ENTRYPOINT [ "/bin/sh" ]
# alias masterpdfeditor4="masterpdfeditor4 > /dev/null 2>&1 &"