# SwiftBar Homebrew Update

This [SwiftBar](https://github.com/swiftbar/SwiftBar) plugin let's you update `formulae` and `casks`.

SwiftBar is a successor to [xbar](https://github.com/matryer/xbar) which this plugin was orginally wrote for.

## Install

I assume you plugin folder is set to `~/.swiftbar/`

Download and install the plugin:

```shell
mkdir "~/.swiftbar/homebrew-update"
wget -qO- https://github.com/mietzen/swiftbar-homebrew-update-plugin/archive/refs/heads/main.tar.gz | tar xvz -C "~/.swiftbar/homebrew-update" --strip-components=1
```

### Working with "sudo" casks

To make this work with `casks` that need `root` access to be installed, the easiest way is to enable `sudo` via touch-id:

```shell
cat << 'EOF' >> ~/.zshrc

# Enable touch-id for sudo
enable-sudo-touch-id() {
    if ! grep -c pam_tid.so /etc/pam.d/sudo &> /dev/null; then
        echo "Enable sudo via Touch ID"
        sudo cp /etc/pam.d/sudo /etc/pam.d/sudo.bak
        awk -v text="auth       sufficient     pam_tid.so" '!/^#/ && !p {print text; p=1} 1' /etc/pam.d/sudo | sudo tee /etc/pam.d/sudo &> /dev/null
    fi
}
enable-sudo-touch-id

EOF
exec zsh
enable-sudo-touch-id
```

## Usage

![Menu Demo](assets/menu.png)

If you click on a `formula` or `cask` a Terminal opens to upgrade the specific `formula` or `cask`. You can also click on `Upgrade All` to update all listed `formulae` and `casks`.
