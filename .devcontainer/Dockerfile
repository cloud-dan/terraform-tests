FROM python:3

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN apt-get update \
    && apt-get -y install --no-install-recommends sudo fonts-powerline apt-utils git zsh build-essential \
    # Clean up
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

# Create a non-root user
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
    # Add sudo support for the non-root user
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

USER $USERNAME

# Setup powerlevel 10k
RUN sudo sed s/required/sufficient/g -i /etc/pam.d/chsh \ 
    && sh -c "$(wget -O- https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)" "" --unattended \
    && git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k \
    && echo "source ~/powerlevel10k/powerlevel10k.zsh-theme" >>~/.zshrc \
    && cd ~/powerlevel10k \
    && exec zsh

COPY .zshrc /home/$USERNAME/.zshrc

COPY .p10k.zsh /home/$USERNAME/.p10k.zsh

CMD ["zsh"]