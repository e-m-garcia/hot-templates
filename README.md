# High-Redshift Optimized Templates (HOT)
*Sets of templates for EAZY and Le Phare photometric template fitting at z > 8*

HOT consists of template sets that are optimized for better inference of galactic properties for very high redshift, photometric objects. This is accomplished by asserting hotter gas temperatures of 45K and 60K in star-forming regions for z = 8-12 and z > 12 respectively, resulting in bottom-lighter/top-heavier IMFs. For further details and justification, refer to [the corresponding paper here](<insert link>).

## Instructions for EAZY:

## Instructions for Le Phare:
To set up and run Le Phare, refer to [the main Le Phare repository](https://gitlab.lam.fr/Galaxies/LEPHARE). For prior estimation of redshift and other properties, use the templates and ages specified at the bottom update of [this readme](https://gitlab.lam.fr/Galaxies/LEPHARE/-/blob/master/sed/GAL/BC03_CHAB/README).

To use HOT Templates in Le Phare, simply move the "LePhareHOT" folder into `$LEPHAREDIR/sed/GAL/`. Now, the templates can be used with ages specified in `$LEPHAREDIR/examples/AGE_BC03COMB.dat` (Previous versions of LePhare may have `test` in place of `examples`).

For example, to read the 45K templates (for z between 8 and 12) with parameters suggested for the COSMOS catalog:

`$LEPHAREDIR/source/sedtolib -c $LEPHAREDIR/examples/COSMOS.para -t G -GAL_SED $LEPHAREDIR/sed/GAL/LePhareHOT/45K/FSPS_TIMF_45K.list -GAL_LIB LIB_45K -SEL_AGE $LEPHAREDIR/examples/AGE_BC03COMB.dat`

To create the grid of predicted magnitudes:

`$LEPHAREDIR/source/mag_gal  -c $LEPHAREDIR/examples/COSMOS.para -t G -GAL_LIB_IN LIB_45K -GAL_LIB_OUT HOT_45K -MOD_EXTINC 3,12,3,12 -EXTINC_LAW SB_calzetti.dat,extlaw_0.9.dat -EB_V 0.,0.1,0.2,0.3,0.4,0.5,0.6,0.7 -Z_STEP 0.03,0,6 -EM_LINES PHYS -EM_DISPERSION 0.25,0.5,1,2,4`

To fit objects to the grid, getting redshifts and other properties in the output file (with zero-point adaptation):

`$LEPHAREDIR/source/zphota -c $LEPHAREDIR/examples/COSMOS.para -CAT_IN <galaxy catalog here> -CAT_OUT hot_fit.out -ZPHOTLIB HOT_45K,ALLSTAR_COSMOS,QSO_COSMOS  -ADD_EMLINES 0,100 -AUTO_ADAPT YES`
