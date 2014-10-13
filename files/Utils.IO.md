```java
public final class IOUtils {

        public static void copy(InputStream is, File file) {
                try {
                        FileOutputStream os = new FileOutputStream(file);
                        copy(is, os);
                } catch (FileNotFoundException e) {
                        L.e(e.toString());
                }
        }

        public static void copy(InputStream is, OutputStream os) {
                try {

                        byte buf[] = new byte[1024];
                        int len;
                        while ((len = is.read(buf)) > 0) {
                                os.write(buf, 0, len);
                        }

                } catch (FileNotFoundException e) {
                        L.e(e.toString());
                } catch (IOException e) {
                        L.e(e.toString());
                } finally {
                        close(is);
                        close(os);
                }
        }

        public static void close(Closeable stream) {
                try {
                        if (stream != null) {
                                stream.close();
                        }
                } catch (IOException e) {
                        L.e(e.toString());
                }
        }

        public static InputStream getStream(String url) {

                InputStream is = null;
                try {
                        is = new URL(url).openConnection().getInputStream();
                } catch (MalformedURLException e) {
                        L.e(e.toString());
                } catch (IOException e) {
                        L.e(e.toString());
                }

                return is;
        }

        public static String toString(InputStream inputStream) {
                BufferedReader br = new BufferedReader(new InputStreamReader(inputStream));
                StringBuilder total = new StringBuilder();
                String line;
                try {
                        while ((line = br.readLine()) != null) {
                                total.append(line);
                        }
                } catch (IOException e) {
                        L.e(e.toString());
                }

                return total.toString();
        }
}
```
