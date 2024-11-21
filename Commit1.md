<p>This is the complete pipeline for the project</p>

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

