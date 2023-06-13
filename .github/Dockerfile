FROM julia:1.9.1

# Julia config
ENV JULIA_CI true
ENV JULIA_NUM_THREADS "auto"
# Let PythonCall use built-in python
ENV JULIA_CONDAPKG_BACKEND "Null"
ENV JULIA_PATH /usr/local/julia/
ENV JULIA_DEPOT_PATH /srv/juliapkg/
ENV PATH ${JULIA_PATH}/bin:${PATH}

# Julia environment
COPY Project.toml Manifest.toml ./

RUN julia --color=yes --project="" -e 'using Pkg, InteractiveUtils; versioninfo(); Pkg.add("IJulia")' && \
    julia --color=yes --project=@. -e 'import Pkg; Pkg.instantiate(); Pkg.resolve(); Pkg.precompile()'
