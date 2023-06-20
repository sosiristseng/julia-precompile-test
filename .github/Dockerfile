FROM python:3.11.4-slim as base

# Supress warnings from parallel
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8

# Julia config
ENV JULIA_CI true
ENV JULIA_NUM_THREADS "auto"
# Let PythonCall use built-in python
ENV JULIA_CONDAPKG_BACKEND "Null"
ENV JULIA_CPU_TARGET "generic;haswell,clone_all;broadwell,clone_all;skylake,clone_all;icelake,clone_all"
ENV JULIA_PATH /usr/local/julia/
ENV JULIA_DEPOT_PATH /srv/juliapkg/
ENV PATH ${JULIA_PATH}/bin:${PATH}
COPY --from=julia:1.9.1 ${JULIA_PATH} ${JULIA_PATH}

FROM base

COPY Project.toml Manifest.toml ./

RUN julia -e 'using InteractiveUtils; versioninfo()' && \
    julia --color=yes --project=@. -e 'import Pkg; Pkg.instantiate(); Pkg.resolve(); Pkg.precompile()'