# Entornos
Clases de entornos de desarrollos

# Creación de un formulario en PowerShell
- Este código permite crear un formulario en PowerShell con una caja de texto y dos botones, uno para cerrar el formulario y el otro para guardar lo que se escriba en la caja de texto en un documento txt.
````
#Formulario
$Form = New-Object System.Windows.Forms.Form
$Form.Text="Formulario"
$Form.Size=New-Object System.Drawing.Size(500,500)
$Form.StartPosition="CenterScreen"
 
#Etiqueta
$Label=New-Object System.Windows.Forms.Label
$Label.Text="Introduce un texto"
$Label.AutoSize=$True
$Label.Location=New-Object System.Drawing.Size(160,160)
 
#Caja de texto
$TextBox = New-Object System.Windows.Forms.TextBox
$TextBox.Location = New-Object System.Drawing.Size(100,180)
$TextBox.Size = New-Object System.Drawing.Size(260,20)
 
#Botón1
$Button1=New-Object System.Windows.Forms.Button
$Button1.Size=New-Object System.Drawing.Size(75,23)
$Button1.Text="Enter"
$Button1.Location=New-Object System.Drawing.Size(120,220)
 
#Botón2
$Button2=New-Object System.Windows.Forms.Button
$Button2.Size=New-Object System.Drawing.Size(75,23)
$Button2.Text="Cerrar"
$Button2.Location=New-Object System.Drawing.Size(220,220)
 
#Funcionalidad para el botón:
#Pulsar Enter almacena en una variable el contenido de la caja de texto y se muestra
#Pulsar Escape sale del formulario
$Button1.Add_Click({
    $TextBox.Text >> Formulario.txt
    $TextBox.Clear()
})
$Button2.Add_Click({$Form.Close()})
 
#Añadir etiqueta
$Form.Controls.Add($Label)
 
#Añadir botones
$Form.Controls.Add($Button1)
$Form.Controls.Add($Button2)
 
#Añadir caja de texto
$Form.Controls.Add($TextBox)
 
$Form.ShowDialog()
````
# Creación de un script para escribir y pulsar un boton
- Este script permite mover el ratón a una posición y hacer clic, después escribirá un mensaje que le digamos y hará clic en el boton para guardar el texto en un documento txt.
````
$MouseEventSig=@'
[DllImport("user32.dll",CharSet=CharSet.Auto, CallingConvention=CallingConvention.StdCall)]
public static extern void mouse_event(long dwFlags, long dx, long dy, long cButtons, long dwExtraInfo);
'@
 
$MouseEvent = Add-Type -memberDefinition $MouseEventSig -name "MouseEventWinApi" -passThru

 
[System.Windows.Forms.Cursor]::Position = New-Object System.Drawing.Point(663,402)
$MouseEvent::mouse_event(0x00000002, 0, 0, 0, 0)
$MouseEvent::mouse_event(0x00000004, 0, 0, 0, 0)

[System.Windows.Forms.SendKeys]::SendWait("abcdefg")

[System.Windows.Forms.Cursor]::Position = New-Object System.Drawing.Point(737,441)
$MouseEvent::mouse_event(0x00000002, 0, 0, 0, 0)
$MouseEvent::mouse_event(0x00000004, 0, 0, 0, 0)
````

