# network simulator
https://github.com/facebook/augmented-traffic-control



echo 'export PATH=/opt/conda/bin:$PATH' | sudo tee /etc/profile.d/conda.sh && \
    wget --quiet https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh



# Create a work space.

# Download miniconda.
echo "Started downloading miniconda"
if [ "${OS_NAME}" = "darwin" ]; then
    MINICONDA_INSTALL_URL="https://repo.continuum.io/miniconda/Miniconda3-latest-MacOSX-x86_64.sh"
else
    MINICONDA_INSTALL_URL="https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh"
fi
curl --location --silent "${MINICONDA_INSTALL_URL}" > "/tmp/miniconda.sh"
echo "Finished downloading miniconda"

# Install miniconda.
echo "Started installing Miniconda"

rm -rf ~/conda/
bash "/tmp/miniconda.sh" -b -p ~/conda
echo "Finished installing Miniconda"


export PATH=~/conda/bin:$PATH
echo "export PATH=~/conda:$PATH" >> ~/.zshrc
echo "export PATH=~/conda:$PATH" >> ~/.bashrc
hash -r
