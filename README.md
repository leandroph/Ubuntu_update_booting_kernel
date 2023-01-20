# Ubuntu: Instalar o Kernel e definir o Default Kernel no GRUB

## Instalação do Kernel

Intalando o kernel default:
```bash
sudo apt install linux-generic
```

## Definindo o Default Kernel no GRUB

1. Encontre a seguinte entrada `/boot/grub/grub.cfg`
    - Obtenha o $menuentry_id_option:
        ```bash
        grep submenu /boot/grub/grub.cfg
        ```
        Exemplo de output:
        ```bash
        submenu 'Advanced options for Ubuntu' $menuentry_id_option 'gnulinux-advanced-4591a659-55e2-4bec-8dbe-d98bd9e489cf' {
        ```
        `'gnulinux-advanced-4591a659-55e2-4bec-8dbe-d98bd9e489cf'` é o que precisamos.
    - Otenha a opção específica do kernel:
        ```bash
        grep gnulinux-4.15.0 /boot/grub/grub.cfg
        ```
        Exemplo de output:
        ```bash
        menuentry 'Ubuntu, with Linux 4.15.0-126-generic' --class ubuntu --class gnu-linux --class gnu --class os $menuentry_id_option 'gnulinux-4.15.0-126-generic-advanced-4591a659-55e2-4bec-8dbe-d98bd9e489cf' {
        ```
        `'gnulinux-4.15.0-126-generic-advanced-4591a659-55e2-4bec-8dbe-d98bd9e489cf'` é o que precisamos.
2. Defina o GRUB_DEFAULT em `/etc/default/grub`
    - Junte as duas strings de entrada obtidas acima por '>', definindo com `GRUB_DEFAULT`.
        ```bash
        GRUB_DEFAULT='gnulinux-advanced-4591a659-55e2-4bec-8dbe-d98bd9e489cf>gnulinux-4.15.0-126-generic-advanced-4591a659-55e2-4bec-8dbe-d98bd9e489cf'
        ```
3. Realize um update no grub
   ```bash
   sudo update-grub
   ```
4. Reinicie a máquina
