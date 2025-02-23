#include <opencv2/opencv.hpp>
#include <iostream>
#include <ctime>

std::string generateFilename() {
    std::time_t now = std::time(nullptr);
    char buffer[100];
    std::strftime(buffer, sizeof(buffer), "snapshot_%Y-%m-%d_%H-%M-%S.jpg", std::localtime(&now));
    return std::string(buffer);
}

int main() {
    cv::VideoCapture cap(0);
    if (!cap.isOpened()) {
        std::cerr << "Error: Could not open webcam" << std::endl;
        return -1;
    }

    cv::Mat frame;
    std::cout << "Press 's' to take a snapshot, 'q' to quit." << std::endl;
    
    while (true) {
        cap >> frame;
        if (frame.empty()) {
            std::cerr << "Error: Empty frame captured" << std::endl;
            break;
        }

        cv::imshow("Webcam Feed", frame);
        char key = cv::waitKey(1);

        if (key == 's') {
            std::string filename = generateFilename();
            cv::imwrite(filename, frame);
            std::cout << "Snapshot saved as " << filename << std::endl;
        } else if (key == 'q') {
            break;
        }
    }
    cap.release();
    cv::destroyAllWindows();
    return 0;
}
