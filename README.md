from PIL import Image

def encrypt_image(image_path, key, output_path):
    img = Image.open(image_path)
    pixels = img.load()

    for i in range(img.width):
        for j in range(img.height):
            r, g, b = pixels[i, j]

            
            r = (r + key) % 256
            g = (g + key) % 256
            b = (b + key) % 256

            pixels[i, j] = (r, g, b)

    img.save(output_path)
    print("Image encrypted and saved as", output_path)


def decrypt_image(image_path, key, output_path):
    img = Image.open(image_path)
    pixels = img.load()

    for i in range(img.width):
        for j in range(img.height):
            r, g, b = pixels[i, j]

            
            r = (r - key) % 256
            g = (g - key) % 256
            b = (b - key) % 256

            pixels[i, j] = (r, g, b)

    img.save(output_path)
    print("Image decrypted and saved as", output_path)




print("1. Encrypt Image")
print("2. Decrypt Image")

choice = input("Enter choice (1/2): ")
key = int(input("Enter key (number): "))

if choice == "1":
    path = input("Enter image path: ")
    encrypt_image(path, key, "encrypted.png")

elif choice == "2":
    path = input("Enter encrypted image path: ")
    decrypt_image(path, key, "decrypted.png")

else:
    print("Invalid choice")
