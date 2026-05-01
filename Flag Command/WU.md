# Flag Command (Hack The Box)

## Challenge Scenario
> Embark on the "Dimensional Escape Quest" where you wake up in a mysterious forest maze that's not quite of this world. Navigate singing squirrels, mischievous nymphs, and grumpy wizards in a whimsical labyrinth that may lead to otherworldly surprises. Will you conquer the enchanted maze or find yourself lost in a different dimension of magical challenges? The journey unfolds in this mystical escape!

## Penyelesaian 
Setelah kita buka challange nya, kita dihadapkan pada sebuah web, dimana ketika sudah mencoba atau mengikuti alur yang ada di game tetap saja tidak menemukan Flagnya. Kita langsung saja buka source code nya, masuk ke bagian `main.js`

Disini, kita memperhatikan ada kode yang agak mencurigakan : 
```
if (availableOptions[currentStep].includes(currentCommand) || availableOptions['secret'].includes(currentCommand)) {
        await fetch('/api/monitor', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({ 'command': currentCommand })
```
Nah, dapat terlihat bahwa disitu ada `secret`

kemudian, saya scroll lagi lihat fungsi yang sekiranya berhubungan, namun tidak ada selain fungsi yang paling bawah : 
```
const fetchOptions = () => {
    fetch('/api/options')
        .then((data) => data.json())
        .then((res) => {
            availableOptions = res.allPossibleCommands;

        })
        .catch(() => {
            availableOptions = undefined;
        })
}
```

Hanya fungsi itu yang memungkinkan pemanggilan data, kita bisa coba lihat data apa saja yang diambil dengan menggunakan console.log()

```
const fetchOptions = () => {
    fetch('/api/options')
        .then((data) => data.json())
        .then((res) => {
            availableOptions = res.allPossibleCommands;
            	console.log(availableOptions);

        })
        .catch(() => {
            availableOptions = undefined;
        })
}
```
 
kemudian, tahap selanjutnya dapat dilihat pada gambar yang ada di Folder ini, bahwa terdapat response seperti berikut : 
```
{allPossibleCommands: {1: ["HEAD NORTH", "HEAD WEST", "HEAD EAST", "HEAD SOUTH"],…}}
allPossibleCommands
: 
{1: ["HEAD NORTH", "HEAD WEST", "HEAD EAST", "HEAD SOUTH"],…}
1
: 
["HEAD NORTH", "HEAD WEST", "HEAD EAST", "HEAD SOUTH"]
2
: 
["GO DEEPER INTO THE FOREST", "FOLLOW A MYSTERIOUS PATH", "CLIMB A TREE", "TURN BACK"]
3
: 
["EXPLORE A CAVE", "CROSS A RICKETY BRIDGE", "FOLLOW A GLOWING BUTTERFLY", "SET UP CAMP"]
4
: 
["ENTER A MAGICAL PORTAL", "SWIM ACROSS A MYSTERIOUS LAKE", "FOLLOW A SINGING SQUIRREL",…]
secret
: 
["Blip-blop, in a pickle with a hiccup! Shmiggity-shmack"]
```

Disitu ada kalimat yang secret yang jika kita masukkan kalimat/command ke dalam web tersebut, maka akan langsung memunculkan Flag nya : 

```
favicon.ico:1  GET http://154.57.164.66:31358/favicon.ico 404 (NOT FOUND)Understand this error
main.js:55 {message: 'HTB{D3v3l0p3r_t00l5_4r3_b35t__t0015_wh4t_d0_y0u_Th1nk??}'}
```

## Flag
`HTB{D3v3l0p3r_t00l5_4r3_b35t__t0015_wh4t_d0_y0u_Th1nk??}`