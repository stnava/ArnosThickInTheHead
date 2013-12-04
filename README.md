ArnosThickInTheHead
===================

prior-based cortical thickness ... in the data directory, do the following:

```
ThresholdImage 3 ch2bet.nii.gz mask.nii.gz 10 1.e9

Atropos -d 3 -x mask.nii.gz -a ch2bet.nii.gz  -i kmeans[3] -o [seg.nii.gz,seg_prob%02d.nii.gz] 

ThresholdImage 3 seg.nii.gz cortex.nii.gz 2 2 

MultiplyImages 3 cortex.nii.gz aal.nii.gz aal_cortex.nii.gz

ResampleImageBySpacing 3 aal_cortex.nii.gz aal_cortex_big.nii.gz 0.5 0.5 0.5 0 0 1 

ImageMath 3 aal_thick.nii.gz LabelThickness aal_cortex_big.nii.gz 

ResampleImageBySpacing 3 aal_thick.nii.gz aal_thicks.nii.gz 1 1 1 0 0 1 

gradd=0.075

th=0.999

KellyKapowski -d 3 -s [seg.nii.gz,2,3] -g seg_prob02.nii.gz -w seg_prob03.nii.gz -o pthick.nii.gz -c [45,0.0,10] -r $gradd -m 1.5 -n 10 -t $th -a aal_thicks.nii.gz

ImageMath 3 aal_thick.nii.gz LabelThickness2 aal_cortex_big.nii.gz 

ResampleImageBySpacing 3 aal_thick.nii.gz aal_thicks2.nii.gz 1 1 1 0 0 1 

KellyKapowski -d 3 -s [seg.nii.gz,2,3] -g seg_prob02.nii.gz -w seg_prob03.nii.gz -o pthick2.nii.gz -c [45,0.0,10] -r $gradd -m 1.5 -n 10 -t $th -a aal_thicks2.nii.gz

KellyKapowski -d 3 -s [seg.nii.gz,2,3] -g seg_prob02.nii.gz -w seg_prob03.nii.gz -o thick.nii.gz -c [45,0.0,10] -r $gradd -m 1.5 -n 10 -t $th 


```
