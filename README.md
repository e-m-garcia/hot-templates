# High-Redshift Optimized Templates (HOT)
*Sets of templates for EAZY and LePhare photometric template fitting at z > 8*

HOT consists of template sets that are optimized for better inference of galactic properties for very high redshift, photometric objects. This is accomplished by asserting hotter gas temperatures of 45K and 60K in star-forming regions for z = 8-12 and z > 12 respectively, resulting in bottom-lighter/top-heavier IMFs. For further details and justification, refer to [the corresponding paper here](<insert link>).  The paper demonstrates the application of templates based on JWST objects in the respective redshift windows.  It also reports the properties of the input stellar populations of the templates.

## Instructions for EAZY:
To use the templates for EAZY, clone or download the "fsps-hot" repository and store in the relevant `templates/` location.  The paths for the `45k` and `60k` sets are relative to this repository, such as in [fsps_45k.param](./eazyHOT/45k/fsps_45k.param) and [fsps_60k.param](./eazyHOT/60k/fsps_60k.param).  To switch to these templates, in EAZY set the parameter `TEMPLATES_PATH` to:

```
TEMPLATES_PATH=templates/hot-templates/eazyHOT/45k/fsps_45k.params
```

or

```
TEMPLATES_PATH=templates/hot-templates/eazyHOT/60k/fsps_60k.params
```

## Instructions for LePhare:
For complete information about LePhare, including set up, usage, and parameter specifications, refer to [the main LePhare repository](https://gitlab.lam.fr/Galaxies/LEPHARE). We suggest starting from parameters derived from the 12 existing BC03 templates used for determining properties of the COSMOS catalogs as shown in [this readme](https://gitlab.lam.fr/Galaxies/LEPHARE/-/blob/master/examples/README). For prior estimation of redshift and other properties, refer to the BC03 commands and parameters in that readme.

To use HOT Templates in LePhare, simply move the "LePhareHOT" folder into `$LEPHAREDIR/sed/GAL/`. Now, the templates should be used with ages specified in `AGE_FSPS_HIGHZ.dat`. You can further reduce this age list in order to eliminate physically impossible star formation (e.g. formation before the beginning of the universe).

The set of templates produced for usage consist of 4 templates at 45K and 60K each of varying star-formation histories (tau and delayed-tau models of 1 and 3 Gyr.) at a z=0.0012 metallicity. These are reconstructed in FSPS (Conroy & Gunn 2010) which allows for replacing the original Chabrier IMF (Chabrier 2003) with a temperature-dependent Kroupa IMF (Kroupa 2001, Jermyn et al. 2018). The templates are written into a BC03 ASCII file format such that LePhare can read them.
