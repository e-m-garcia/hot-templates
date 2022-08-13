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
For complete information about LePhare, including set up, usage, and parameter specifications, refer to [the main LePhare repository](https://gitlab.lam.fr/Galaxies/LEPHARE). The parameters provided in the examples below are taken from suggestions for 12 existing BC03 templates used for determining properties of the COSMOS catalogs as shown in [this readme](https://gitlab.lam.fr/Galaxies/LEPHARE/-/blob/master/examples/README). For prior estimation of redshift and other properties, refer to the BC03 commands and parameters in that readme.

To use HOT Templates in LePhare, simply move the "LePhareHOT" folder into `$LEPHAREDIR/sed/GAL/`. Now, the templates can be used with ages specified in `AGE_FSPS_HIGHZ.dat`. Also note that previous versions of Le Phare may have `test` in place of `examples`.

For example, to read the 45K templates (for z between 8 and 12) with parameters for COSMOS:

```
$LEPHAREDIR/source/sedtolib -c $LEPHAREDIR/examples/COSMOS.para -t G -GAL_SED $LEPHAREDIR/sed/GAL/LePhareHOT/45K/FSPS_TIMF_45K.list -GAL_LIB LIB_45K -SEL_AGE $LEPHAREDIR/sed/GAL/AGE_FSPS_HIGHZ.dat
```

To create the grid of predicted magnitudes:

```
$LEPHAREDIR/source/mag_gal -c $LEPHAREDIR/examples/COSMOS.para -t G -GAL_LIB_IN LIB_45K -GAL_LIB_OUT HOT_45K -MOD_EXTINC 1,4,1,4 -EXTINC_LAW SB_calzetti.dat,extlaw_0.9.dat -EB_V 0.,0.1,0.2,0.3,0.4,0.5,0.6,0.7 -Z_STEP 0.03,0,6 -EM_LINES PHYS -EM_DISPERSION 0.25,0.5,1,2,4
```

To fit objects to the grid, getting redshifts and other properties in the output file (with zero-point spectroscopic adaptation):

```
$LEPHAREDIR/source/zphota -c $LEPHAREDIR/examples/COSMOS.para -CAT_IN <galaxy catalog here> -CAT_OUT hot_fit_45k.out -ZPHOTLIB HOT_45K,ALLSTAR_COSMOS,QSO_COSMOS -ADD_EMLINES 0,100 -AUTO_ADAPT YES
```

The set of templates produced for usage consist of 4 templates at 45K and 60K each of varying star-formation histories at a z=0.0012 metallicity. These are reconstructed in FSPS (Conroy & Gunn 2010) which allows for replacing the original Chabrier IMF (Chabrier 2003) with a temperature-dependent Kroupa IMF (Kroupa 2001, Jermyn et al. 2018). The templates are written into a BC03 ASCII file format such that LePhare can read them.
