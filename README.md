# ImageToGreyImage
Conver Image to Grey Image
<img src="https://raw.githubusercontent.com/jutyarr/ImageToGreyImage/master/screenshotImageGray.PNG" />
//Create a variable of type Bitmap to store the path of uploaded image
 Bitmap bmp;


        
        //Upload button Image wich uploads the image and and assign its path to the first picturebox control then calls the ConverToGray() method
        private void BtnUpload_Click(object sender, EventArgs e)
        {
          OpenFileDialog openFileDialog = new OpenFileDialog();
            openFileDialog.Filter = "Choose a photo (*.jpg; *.png)|*.jpg; *.png |All files (*.*)|*.*";
            if(openFileDialog.ShowDialog() == DialogResult.OK)
            {
                string path = openFileDialog.FileName;
                bmp = new Bitmap(path);
                pictureBox1.Image = bmp;
                ConverToGray();
            }
        }
        
     //This method converts the image to gray   
        private void ConverToGray()
        {
            Bitmap bmp2 = new Bitmap(bmp);
            if (bmp == null)
            {

                MessageBox.Show("Please first upload an Image file", "Warning");
                return;
            }
            int h = bmp.Height;
            int w = bmp.Width;

            for (int y = 0; y < h; y++)
            {
                for (int x = 0; x < w; x++)
                {
                    Color pixColor;
                   var currentPixColor = bmp.GetPixel(x, y);
                    int a = currentPixColor.A;
                    int r = currentPixColor.R;
                    int g = currentPixColor.G;
                    int b = currentPixColor.B;
                    int avg = (r + g + b) / 3;
                    pixColor = Color.FromArgb(a, avg, avg, avg);
                    bmp2.SetPixel(x, y, pixColor);

                }
            }
            pictureBox2.Image = bmp2;
        }
