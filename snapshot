import os
import cv2
import time
import multiprocessing

def capture_frame(frame_info):
    frame_number, frame, output_folder = frame_info
    timestamp = time.strftime("%Y%m%d_%H%M%S", time.localtime())
    output_filename = os.path.join(output_folder, f"frame_{frame_number:05d}_{timestamp}.jpg")
    cv2.imwrite(output_filename, frame)
    print(f"Captured frame {frame_number}")

def capture_frames(input_video, output_folder, interval_seconds=60):
    if not os.path.exists(input_video):
        raise FileNotFoundError("Input video not found.")

    if not os.path.exists(output_folder):
        os.makedirs(output_folder)

    video_capture = cv2.VideoCapture(input_video)
    fps = video_capture.get(cv2.CAP_PROP_FPS)
    interval_frames = int(fps * interval_seconds)

    frame_number = 0
    while True:
        video_capture.set(cv2.CAP_PROP_POS_FRAMES, frame_number)
        ret, frame = video_capture.read()
        if not ret:
            break

        timestamp = time.strftime("%Y%m%d_%H%M%S", time.localtime())
        output_filename = os.path.join(output_folder, f"frame_{frame_number:05d}_{timestamp}.jpg")
        cv2.imwrite(output_filename, frame)
        print(f"Captured frame {frame_number}")

        frame_number += interval_frames

    video_capture.release()
    print(f"Total frames captured: {frame_number}")

if __name__ == "__main__":
    input_video = r"D:\Codes\snapshot\1.mp4"  # Replace with the actual path of your input video file
    output_folder = r"D:\Codes\snapshot"          # Replace with the desired output folder name

    capture_frames(input_video, output_folder)
