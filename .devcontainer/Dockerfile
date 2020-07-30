FROM python:3

RUN apt-get update && apt-get install -y \
    apt-utils \
    zsh \
    build-essential

RUN  wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh || true

COPY .zshrc /root/.zshrc

CMD ["zsh"]