FROM hashicorp/terraform:light

RUN apk add zsh

RUN wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true

COPY .zshrc /root/.zshrc

CMD ["zsh"]