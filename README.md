# Standard CI Build Flow

This directory documents the source-driven CI build surface. The CI scripts are separate from the older local daily bring-up scripts.

Principles:

- Rootfs construction is parameterized by workflow inputs and environment variables.
- Boot/GRUB image construction is parameterized by declared kernel, DTB, BOOTAA64.EFI and GRUB build inputs.
- Device policy checks are not embedded into the rootfs builder.
- Build outputs always include manifests and SHA256SUMS.
- Release upload is optional and controlled by the workflow input `release_tag`.

Primary workflow:

- `.github/workflows/build-rootfs-and-grub.yml`

Primary scripts:

- `scripts/ci/build-rootfs-image.sh`
- `scripts/ci/build-grub-image.sh`
- `scripts/ci/pack-disk-image.sh`

Important workflow inputs include:

- `username`, `user_password`, `root_password_mode`, `root_password`, `user_sudo_mode`
- `rootfs_partlabel`, `rootfs_uuid`, `rootfs_image_size`, `boot_image_size`, `boot_fat_label`
- `kernel_artifact_archive_url`, `bootaa64_efi_url`, `grub_build_archive_url`, `dtb_name`
- `root_selector`, `rootargs`, `rootargs_extra`, `stableargs`

The optional `overlay_archive_url` and `deb_archive_url` inputs are the standard way to feed device-specific payloads into the rootfs without hardcoding a specific verified baseline in the builder.
