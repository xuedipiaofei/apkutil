apkutil
=======

Apk Utility


## Make pakcage for iSoftLinux

```
makepkg -g
makepkg -f
```


## TODO

- [ ] migrated to libpng-1.6.7
      * struct png_struct_def have been privated
      * png_set_gray_1_2_4_to_8 have been replaced with png_set_expand_gray_1_2_4_to_8
      * png_sizeof have been removed
