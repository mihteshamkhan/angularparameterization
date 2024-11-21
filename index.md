<H1> Angular Parameterization in a Timepix3 detector using a Convolutional Neural Network</H1>

<H1> Building Geant4Medipix </H1>

<p> The first step is to install all dependencies.</p>

<H2> Basics </H2>

<pre><code>sudo apt install git</code></pre>

<H2> Build Essentials </H2>

<p> Since both Geant4 and G4Medipix are built on top of C++/C, it makes sense to install the build essentials. Please make sure to get the versions correct. Geant4Medipix strictly follows C++11 standard. </p>

<pre><code>sudo apt install g++-11
sudo apt install gcc-11
sudo apt install make
sudo apt install cmake-curses-gui</code></pre>

<H2> Prerequisites </H2>

<p>Now we will install the packages and libraries needed to build Geant4Medipix.</p>
<H3>Geant4 </H3>

<p> We will install Geant4 v11.1.0 using spack. Please make sure to add spack to path after installation.</p>

<pre><code>git clone https://github.com/spack/spack.git ~/spack</code></pre>
<p> To speed up the building process, we can can set the number of cores N <p>
<pre><code>export SPACK_BUILD_JOBS= N </code></pre>
<p> And finally, we install Geant4 v11.1.0</p>
<pre><code>spack install geant4@11.1.0</code></pre>

<p> As before, make sure to add Geant4 to path.</p>

<H3> Boost </H3>

<pre><code>sudo apt install libboost-all-dev</code></pre>

<H3> HDF5 </H3>

<pre><code> sudo apt install libhdf5-dev </code></pre>

<H2> Geant4Medipix </H2>

<p> Finally, we are all set to build Geant4Medipix. <p>

<pre><code> git clone https://github.com/juseus03/geant4medipix </code></pre>
<p> To make sure ccmake uses the correct standard, </p>

<pre><code>ccmake -DCMAKE_CXX_STANDARD=11 PATH</code></pre>
<p> Follow the configure, release, generate pattern, and finally,
<pre><code>make -j N</code></pre>

<p> Finally we have Geant4Medipix built and ready to use. Make sure to add Geant4Medipix to path. </p>

<H1>Deep Learning Pipeline</H1>

<p>At this point, I will consider that you were able to successfully generate your simulation data (as .h5 file(s)). Now, we proceed to the deep learning pipeline for the project.</p>

<h2>Essentials</h2>
<p> We need conda! The python scripts we will be using work with particular version(s) of Tensorflow and Keras and those versions require certain version(s) of Python. If you are not as good as building python from scratch like me, conda is a good option.</p>

<pre><code>wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh</code></pre>
<pre><code>bash Miniconda3-latest-Linux-x86_64.sh</code></pre>

<p>Now we can simply have the required python (and pip) version using:</p>

<pre><code>conda create -n myenv python=3.6</code></pre>
<pre><code>conda activate myenv</code></pre>

<p> There you have it. Now you should successfully have:
python version: Python 3.6.13 :: Anaconda, Inc.
pip version: pip 21.2.2 </p>

<h2>Prerequisites</h2>
<p>Now that we have the right python environment, we can move to more serious installations.</p>

<pre><code>pip install numpy==1.14.5</code></pre>
<pre><code>pip insall scipy==1.1.0</code></pre>
<pre><code>pip install h5py==2.8.0</code></pre>
<pre><code>pip install tensorflow==1.4</code></pre>
<pre><code>pip install keras==2.1</code></pre>

<p>Or you can reverse engineer from:</p>

<pre><code>pip install -r requirements.txt</code></pre>

<p> where the requirements.txt contains:
bleach==1.5.0
certifi==2021.5.30
dataclasses==0.8
enum34==1.1.10
h5py==2.8.0
html5lib==0.9999999
importlib-metadata==4.8.3
Markdown==3.3.7
numpy==1.14.5
protobuf==3.19.6
scipy==1.1.0
six==1.16.0
tensorflow==1.4.0
tensorflow-tensorboard==0.4.0
typing_extensions==4.1.1
Werkzeug==2.0.3
zipp==3.6.0 </p>

<H2> Training </H2>

<p> Now that our environment is all set, we can finally clone the python script and train our model. You can download the script as:</p>

<pre><code>wget https://raw.githubusercontent.com/M4I-nanoscopy/tpx3-event-localisation/refs/heads/master/deeplearning/training.py</code></pre>

<p> Now, we can easily train the model on our simulation data .h5 file. This script can take several arguements. The most important ones are --tot , --toa , --epochs N </p>

<pre><code>python training.py PATH(to .H5 file) --model PATH(to save the model .h5 file) --arguments</code></pre>
